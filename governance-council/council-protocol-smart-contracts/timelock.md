# Timelock

* **Contract Name:** Timelock.sol
* **Type/Category:** Governance
* **Contract Source:**[https://github.com/element-fi/council/blob/main/contracts/features/Timelock.sol](https://github.com/element-fi/council/blob/main/contracts/features/Timelock.sol)

## **1. Introduction (Summary)**

The timelock is a speed bump for calls. It requires calls to wait for a period before they can be executed. After a call is registered, the call can be removed during the waiting period, and an authorized address can extend the waiting period only once.

## **2. Contract Details**

* The key functions in the time lock are the ability for an owner to register a call via a 32 byte hashed identifier, to remove the registered call, to allow anyone to run that call after a customizable period of time, and the ability for authorized addresses to add an optional one time delay in addition to the regular delay in the contracts.
* The state in the timelock is a mapping of registered calls to execution timestamps, authorized addresses, and an address that can register calls.

## **3. Key Mechanisms & Concepts**

The timelock is a mechanism to ensure that any security-critical votes that execute a call or bundle of calls have a minimum review time to allow the community to check that the calls have no unintended side effects. After the core voting contract votes something that is high security-critical, a hash of the information of the calls to be executed will be registered with the timelock.

After waiting a minimum amount of time, anyone can call the timelock to execute the call or set of calls. Suppose the proposal is reviewed and an error is identified during the review period. In that case, the core voting contract must vote again to remove the call from the timelock. Because core voting has a minimum vote time, the effective timelock period is the timelock period minus the minimum voting time. To mitigate this, authorized addresses \[such as the GSC] can do a one-time per call increase in lock time for a registered call. The time bump should be slightly more than the minimum voting time to enable removal votes.

The timelock can upgrade its stored parameters such as the delay time and the amount of bump time by making a call to itself which sets these pieces of information.

## **4. Gotchas (Potential source of user error)**

* Calls registered with the contract must all succeed or the whole bundle will fail.
* Calls cannot re-access the timelock as a reentrancy lock protects it.
* Timelocks should not be used for emergency mitigation functionality and security response functionality, such as pause controls. Because of the slowdown, they may not be able to respond to disclosures of security bugs in time.

## **5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)**

Since the timelock controls its parameters, the timelock can upgrade itself to a non-functional state by, for instance, making the address that registers calls one which cannot send transactions that register calls or setting the delay to a very large number. Parameter setting should be done with a high amount of care.
