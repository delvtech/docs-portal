# User Proxy

* **Contract Name:** UserProxy
* **Type/Category:** Core/Proxy
* **Associated System Diagram**: n/a
* **Contract Source:** [https://github.com/delv-tech/elf-contracts/blob/main/contracts/UserProxy.sol](https://github.com/delv-tech/elf-contracts/blob/main/contracts/UserProxy.sol)

## 1. Overview

The User Proxy is a user convenience contract that consolidates the actions needed to create the principal and interest tokens. It facilitates deposits and withdrawals from and to available tranches.

### **Glossary**

* **Tranche:** The contract which locks wrapped Yearn shares and mints yield and principal tokens.

## 2. Contract Details

### **Key Functionality:**

* `mint`: Mints a Principal/Interest token pair from either underlying token or ETH, then returns the tokens to the caller. This function assumes that it already has an allowance for the token in question. This function also accepts an encoded array of permit calls to make prior to minting. This permit call can be used with tokens like USDC and give the contract an allowance before the mint.
* `withdrawWeth`: Allows a user to withdraw and unwrap WETH in the same transaction likely quite a bit more expensive than direct unwrapping but useful for those who want to do one transaction instead of two. This function accepts an encoded array of permit calls as well.

**Storage:** This contract stores the variables needed to derive Tranches, as well as a state variable governing the usability of the contract.

## 3. Key Mechanisms & Concepts

The User Proxy can be frozen by an authorized address for any reason, it can also be deprecated by the owner. This will completely destroy the contract.

## 4. Gotchas (Potential source of user error)

A call to `withdrawWeth` in order to withdraw and unwrap the WETH can be more expensive than a manual withdrawal followed by an unwrapping. The only benefit is that it is conveniently done in a single function.

## 5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)

If the `isFrozen` flag is flipped on, the contract will not be able to operate.
