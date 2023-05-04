# History

* **Contract Name:** History.sol
* **Type/Category:** Library
* **Contract Source:**[https://github.com/delv-tech/council/blob/main/contracts/libraries/History.sol](https://github.com/delv-tech/council/blob/main/contracts/libraries/History.sol)

## **1. Introduction (Summary)**

The History library is an optimized data structure that uses the custom storage layout of our proxy architecture to store historical block indexed data for an address. It is used to track delegation in the Locking Vault, Vesting Vault, and potentially future voting vaults.

## **2. Contract Details**

The History library allows mapping from addresses to arrays containing historical data based on a name. This follows the pattern of the custom storage library for proxy storage. When data is added for a user, it is appended to the end of their stored data. Calls to 'find' or 'findAndClear' do a binary search over the stored historical data to return data at the greatest block number less than or equal to the queried one. The 'findAndClear' call also deletes data with block numbers older than some threshold.

Since this contract is a library, it does not hold any storage. Still, it allows a caller to define a storage mapping, which is a mapping from an address to a custom encoded historical data array.

## **3. Key Mechanisms & Concepts**

The voting vault delegation and voting system need the past state of the voting power at the start of the voting period; this library helps get that. Each voting vault that uses delegation inherits from this library and uses its internal methods when called by governance to lookup the past voting power of each user.

## **4. Gotchas (Potential source of user error)**

* Lookups revert on the access of uninitialized data. Contracts should not depend on zero return for users who have never had voting power added.
* Like the storage library, this library has direct access to storage and the possibility to corrupt storage. We recommend very high caution using this in combination with another assembly.
* If the voting vault must select a stale data-bound greater than the data it looks up, 'findAndClear' can cause reverts.

## **5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)**

* If a delegatee gains more than a very high threshold of entries, they may pass a threshold where calling 'findAndClear' for them will cost more gas than the block limit. This is highly unlikely and can be mitigated by the user withdrawing.
