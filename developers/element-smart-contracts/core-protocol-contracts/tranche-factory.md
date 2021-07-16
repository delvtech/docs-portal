# Tranche Factory

* **Contract Name:** TrancheFactory
* **Type/Category:** Core
* **Associated System Diagram**: n/a
* **Contract Source:** [https://github.com/element-fi/elf-contracts/blob/main/contracts/factories/TrancheFactory.sol](https://github.com/element-fi/elf-contracts/blob/main/contracts/factories/TrancheFactory.sol)

## 1. Overview

The Tranche Factory creates new Tranches on existing wrapped position addresses. Deployment of new factories is done using CREATE2. This allows for cheap on-chain verification that a factory was deployed by this contract. It also allows for cheap tranche address derivation.

### **Glossary**

* **Tranche:** The contract which locks wrapped Yearn shares and mints yield and principal tokens.
* **Wrapped position:** Wrapped shares of a yearn vault.

## 2. Contract Details

### **Key Functionality:**

`deployTranche`: Deploys a new tranche given an expiration time and the address of the wrapped position contract.

## 3. Gotchas \(Potential source of user error\)

This contract uses CREATE2 to deploy the tranche, therefore redeployment of a tranche with the same expiration and wrapped position address will fail.

