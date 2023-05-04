# Yearn Vault Asset Proxy

* **Contract Name:** YVaultAssetProxy
* **Type/Category:** System/Integration
* **Associated System Diagram**: n/a
* **Contract Source:** [https://github.com/delv-tech/elf-contracts/blob/main/contracts/YVaultAssetProxy.sol](https://github.com/delv-tech/elf-contracts/blob/main/contracts/YVaultAssetProxy.sol)

## 1. Overview

The YVaultAssetProxy contract implements WrappedPosition and performs the actual deposits into the yearn vaults. It also handles the local reserves in case an actual deposit is not needed.

### **Glossary**

* **Yearn position:** The value an address controls in a yearn vault
* **Underlying token:** The token accepted by the yearn vault. (eg: USDC for the USDC yearn vault)
* **Wrapped position token:** The token minted by the Wrapped position contract after depositing.
* **Reserves:** Value deposited to the contract by a third party used to amortize deposit cost by avoiding yearn interaction on small deposits and withdrawals.

## 2. Contract Details

### **Key Functionality:**

* `reserveDeposit`: Deposit value to the local reserves.
* `reserveWithdraw`: Withdraw value from the reserves.
* `_deposit`: This internal function deposits the underlying tokens to the yearn vault and returns the shares received and the amount deposited. Assumes the underlying tokens were transferred to this contract before this function was called. If the local reserves are sufficient, then they are used instead and a direct yearn deposit is avoided.
* `_withdraw`: This internal function withdraws yearn shares from the vault. If the local reserves are sufficient then there is no actual withdrawal.

**Storage:** The only storage in this contract is related to the yearn vault. The vault address and vault decimals are stored.

## 3. Key Mechanisms & Concepts

The `YVaultAssetProxy` uses local reserves to amortize deposit and withdrawal costs. In order to achieve lower costs, each `YVaultAssetProxy` must be funded with underlying the tokens.

## 4. Gotchas (Potential source of user error)

Depositing value in the reserve could earn interest, but there is no guarantee that any interest will be earned at all.&#x20;
