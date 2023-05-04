# Vesting Vault

* **Contract Name:** VestingVault.sol
* **Type/Category:** Voting Vault/Governance
* **Contract Source:** [https://github.com/delvtech/council/blob/main/contracts/vaults/VestingVault.sol](https://github.com/delvtech/council/blob/main/contracts/vaults/VestingVault.sol)

## **1. Introduction (Summary)**

The vesting vault contract is used to set up long-term grants for core contributors to the Element ecosystem, but its flexible approach enables it to be used for many other types of grants as well. It is also a voting vault so that community members can vote with vested but unclaimed tokens and unvested tokens.

## **2. Contract Details**

#### **Key Functionalities:**

* Ability to create grants which release over time with an optional cliff.
* Ability to remove grants for exited contributors.
* Grant holders should be able to vote and delegate votes with their locked tokens.
* Grant holders should be able to claim their tokens on schedule.

#### **State:**

* A mapping tracking of the historical voting power.
* A mapping tracking grants.
* Contract solvency information.
* Ownership information.

## **3. Key Mechanisms & Concepts**

The contract allows a manager to create vesting grants using a balance of tokens that are stored in the contract. Each grant has a non-vesting period, and an optional cliff followed by a linear vesting period. The created grants cannot add up to a total amount more than what is in the contract. Each grant holder can delegate their votes to other addresses, and the contract state keeps a record of historical votes that are compatible with the core voting contract requirements. In addition to a historical voting power record, the contract also stores user grants in a mapping. When a grant is removed for a contributor, any unlocked tokens are transferred to them, and their grant is removed.

## **4. Gotchas (Potential source of user error)**

* The grant administrator cannot create more outstanding grants than the token which have been deposited. They must use the deposit method for that deposit to be recognized.
* Any tokens or ETH directly transferred to the contract cannot be removed and are locked forever.

## **5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)**

* The vesting vault contract should only be operated as an upgradeable proxy component because the storage library used is intended for that application.
* In the case of compromise of the grant funding address, all funds in this contract are at risk. And, in the case of compromise of the upgrade system, all funds in this contract are at risk.
