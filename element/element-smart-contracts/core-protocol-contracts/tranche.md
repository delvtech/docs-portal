# Tranche

* **Contract Name:** Tranche
* **Type/Category:** Core
* **Associated System Diagram**: n/a
* **Contract Source:** [https://github.com/element-fi/elf-contracts/blob/main/contracts/Tranche.sol](https://github.com/element-fi/elf-contracts/blob/main/contracts/Tranche.sol)

## 1. Overview

The Tranche contract locks wrapped position shares and mints yield and principal tokens in return. These tokens can be redeemed on Tranche (term) expiration.

### **Glossary**

* **Yield Bearing Asset (YBA): **An asset that increases in value, for example, Vault shares.
* **Underlying token:** The token used by the yield bearing asset to generate yield. (eg: USDC for USDC yearn vault shares)
* **Yield Token (YT): **Token representing the yield earned by the deposited wrapped yield bearing assets.
* **Principal Token (PT):** The token representing the initial deposited value of the wrapped yield bearing assets shares.
* **Wrapped position:** Wrapped Yield Bearning Asset.

## 2. Contract Details

### **Naming Conventions:**

This contract also acts as the Principal Token (PT). The name of the principal token is assembled as the following example `eP:yUSDC:03:JAN-2021:GMT`

* `eP` States that this is the Principal token.
* `yUSDC` This is the Yield Bearing Asset.
* `03:JAN-2021:GMT` This is the expiration of the Tranche, after which the token can be redeemed.

### **Key Functionality:**

* `deposit`: This function receives underlying tokens, converts them to wrapped position tokens, and mints YTs and PTs in return. If the Tranche contract contains wrapped position tokens that have earned interest after they were deposited, then the amount of PT minted will be reduced to pay for that accrued interest. This function requires the caller to set an appropriate underlying token allowance to this contract.
* `prefundedDeposit`: This functions the same way as the`deposit`, however, it assumes that the underlying tokens have already been transferred to this contract. This function does not require an allowance.
* `withdrawPrincipal`: Withdraw a specified amount of principal tokens and receive a corresponding amount of underlying tokens. This function can only be called after the tranche expiration.
* `withdrawInterest`: Withdraw a specified amount of yield tokens and receive a corresponding amount of underlying tokens. This function can only be called after the tranche expiration.

**Storage:** This contract directly extends an ERC20 token which functions as the PT and stores:

* The address of the interest token (YT)
* Information related to the YBA such as the address, underlying token address, and underlying token decimal precision.
* Values used for internal accounting related to user balance, the total value supplied, and the interest token supplied.
* Miscellaneous variables are used for unlocking and securing the contract from edge cases.

## 3. Key Mechanisms & Concepts

* This contract directly extends the ERC20 token used as PT. This means that this contract's address is also the PTs address. unlike the PT, the YT is an external contract set on construction.
* If the yield bearing assets held by this contract have accrued negative interest after the Tranche has expired, then a withdrawal block of 48 hours takes place. If interest rates go back above zero during this period, then the contract resumes normal function. If interest rates stay negative, then the withdrawn principal tokens will be redeemable pro-rata for the holdings of the contract after the wait block ends.

## 4. Gotchas (Potential source of user error)

* `PrefundedDeposit` will use all underlying tokens available to the Tranche contract at that time, therefore the call that `transferstokens` to the Tranche contract must be called in the same transaction as PrefundedDeposit, or the funds could be unintentionally stolen by the next call to this function.

## 5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)

Failure conditions are very closely related to those of the underlying YBA. If the YBA loses all value due to a hack or a black swan event then the YTs and PTs will not be withdrawable for any value.
