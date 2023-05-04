# Locking Vault

* **Contract Name:** LockingVault.sol
* **Type/Category:** Voting Vault/Governance
* **Contract Source:** https://github.com/delvtech/council/blob/main/contracts/vaults/LockingVault.sol

## **1. Introduction (Summary)**

The Locking vault is a contract that allows the DAO to allocate votes to the token holders. It works by having the holders of the token deposit them into the Locking Vault. After votes have been allocated to users, they can then delegate votes to other addresses to vote on their behalf. To use their tokens in other contexts, the users must withdraw them from the locking vault.

## 2. Contract Details

#### Key Functionalities:

* Users can deposit into the locking vault and then either be allocated votes or have their votes be delegated to another address.
* Users can change which address their votes are delegated to.
* Users can withdraw their tokens to move them back into their wallets.
* The core voting contract can query the LockingVault to check the historical voting power of users in it.

#### Storage Layout:

* A system of state which tracks the historical power of addresses using the logic of the History.sol library.
* A mapping that tracks a user's deposited amount and who they have delegated to.
* Configuration parameters such as the token used and how much voting power history to retain.

## 3. Key Mechanisms & Concepts

The Council DAO framework can allocate votes to multiple sources but cannot employ the Compound governance contracts technique that tracks voting power inside the ERC20 itself. Therefore, for a user to have their voting power recognized, they must deposit into the voting contracts. This contract enables a user to deposit their tokens and receive voting power. When they deposit, they are allowed to select an address that may vote with their voting power. Each address has a historical tracker of voting power indexed by block number, and when they deposit or are delegated to the historical tracker records this. The core voting contract then calls the locking vault to ask how many votes an address has when a user votes on a proposal.

## 4. Gotchas (Potential source of user error)

* A user can fund another user's account and, on deposit, select the first delegation address. The 'firstDelegation' field in the call after the first call is ignored.
* If a malicious actor deposits to another user's address before that user deposits, then that malicious actor can select the delegation for the user. If the user deposits, they should confirm they have not been front run and, if they have, they must change delegation.
* Vote power queries will revert for users who have never been deposited or delegated to.

## 5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)

* The Locking Vault contract is intended to be used as the logic contract for an upgradable proxy, and it is recommended that it be only used in this context.
* Since the Locking Vault is upgradable, its funds have the same risk profile as the governance system as a whole.
* In the case of a bug, the governance system should upgrade the locking proxy to protect user funds. However, because the locking vault is a primary source of funds, certain critical bugs may compromise its ability to do so.
