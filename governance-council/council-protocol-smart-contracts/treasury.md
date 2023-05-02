# Treasury

* **Contract Name: Treasury.sol**
* **Type/Category:** Treasury/Governance
* **Contract Source:**[https://github.com/delv-tech/council/blob/main/contracts/features/Treasury.sol](https://github.com/delv-tech/council/blob/main/contracts/features/Treasury.sol)

## **1. Introduction (Summary)**

The Treasury contract is an isolated holder of Element governance funds that allows an authorized address to move them. This isolation improves the security of the system and prevents a bug from compounding to total fund loss.

## **2. Contract Details**

The contract only contains the functionality to allow an authorized address to move the ERC20 and ETH tokens it contains; to set ERC20 allowances or to make generic calls. The stored data is the authorized address.

## **3. Key Mechanisms & Concepts**

The contract receives a call from an address and then checks if it is authorized to move funds. If the address is authorized, it makes an ERC20 transaction that can move funds or set allowances.

## **4. Gotchas (Potential source of user error)**

* Sending the funds to the wrong address (person or contract) or approving the wrong contract can result in the loss of funds.

## **5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)**

* It is important to note that, if the ownership of the contract is reset, it should be reset to an address that can make calls or the funds in the treasury will be frozen in place.
