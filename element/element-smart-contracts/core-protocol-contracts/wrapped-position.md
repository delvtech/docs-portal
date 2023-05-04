# Wrapped Position

* **Contract Name:** WrappedPosition
* **Type/Category:** Core
* **Associated System Diagram**: n/a
* **Contract Source:** [https://github.com/delvtech/elf-contracts/blob/main/contracts/WrappedPosition.sol](https://github.com/delvtech/elf-contracts/blob/main/contracts/WrappedPosition.sol)

## 1. Overview

The Wrapped Position is an abstract contract that wraps a yield-bearing Asset (YBA) such as Yearn shares.

### **Glossary**

* **Yield Bearning Asset (YBA):** An asset that increases in value, for example, Yearn Vault shares.
* **Underlying token:** The token used by the yield-bearing asset to generate yield. (eg: USDC for USDC yearn vault shares)
* **Wrapped position token:** The token minted by the Wrapped position contract after depositing.

## 2. Contract Details

### **Key Function**ality:&#x20;

* `deposit`: The Entry point. It receives the underlying token and mints ERC20 tokens equal to the YBA shares received from that deposit. The caller must approve the wrapped position contract to use the underlying token before a call to deposit. Note that the vault deposit does not happen here. It is delegated to the extending contract
* `prefundedDeposit`: Functions like the deposit function, except it assumes the underlying tokens were transferred to the wrapped position contract before this function was called. We do not need to approve the wrapped position contract to use the underlying tokens in this case.
* `withdraw`: The Exit point. It burns wrapped position tokens to return underlying tokens. The actual contract interaction logic is delegated to the extending contract.

**Storage:** There is no stored state other than the underlying token.&#x20;

## 3. Key Mechanisms & Concepts

The WrappedPosition contract abstractifies deposit and withdrawal logic associated with the WrappedPosition ERC20, however, it is an abstract contract and therefore cannot be used on its own.

## 4. Gotchas (Potential source of user error)

`PrefundedDeposit` will use all underlying tokens available to the Wrapped Position at that time, therefore the call that transfers the shares must be called in the same transaction as the ERC20 transaction which funds a deposit or the funds could be unintentionally stolen by the next call to this function.
