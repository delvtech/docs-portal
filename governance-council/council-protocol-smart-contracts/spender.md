# Spender



* **Contract Name:** Spender.sol
* **Type/Category:** Treasury/Governance
* **Contract Source:**[https://github.com/element-fi/council/blob/main/contracts/features/Spender.sol](https://github.com/element-fi/council/blob/main/contracts/features/Spender.sol)

## **1. Introduction (Summary)**

The spender contract is designed to leverage the variable quorum requirements of the core voting contract to enable a very small-scale grant program.

## **2. Contract Details**

#### **Key Functionalities:**

* Spend a number of tokens up to a high, medium, or low threshold via separate functions for high, medium, and low spends.
* Allow the owner to remove the tokens from this contract.

**State:**

* High, medium, and low spending thresholds
  * Tracking the block by historical block spending ensures that a threshold is violated in no block.

## **3. Key Mechanisms & Concepts**

The contract contains some tokens and then allows an owner address to spend tokens from this contract. The owner of the contract will be the core voting contract. In the core voting contract, each of the spending functions should be given its own quorum. In this setup, this contract enables small and correspondingly low-security grants to fund non-contentious community-driven projects which are low expenditure.

## **4. Gotchas (Potential source of user error)**

The expenditure in each block is tracked in aggregate, so if a low spend is successful, a following high spend in the same block can only spend up to (high spend bound - low spend bound).

## **5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)**

In the case of contract failure, the owner should remove funds from the contract.
