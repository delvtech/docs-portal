# Voting Vaults

### Overview

Voting Vaults provide the ability to assign voting power to specific types of tokens/positions. The result is beautiful — governance users can maximize capital efficiency while maintaining the ability to delegate or vote when the time comes. Voting vaults are designed to be upgraded, allowing for voting vault logic to be updated by governance and to avoid the pains that come with governance upgrade migrations.

The creation of a voting vault begins with defining a strategy for counting votes / providing voting power. Once the logic has been established, governance will vote to approve the method, and if successful, the integration is complete, and users can start voting.

### The First Voting Vaults

The first voting vault contracts that will allocate voting power in the Element governance system are ones whose mechanisms are familiar to most people who have participated in past or current DAO governance: locking and vesting vaults.

#### **The Locking Vault**

The locking vault allows users to deposit their tokens into a contract in exchange for voting power, which can also be delegated to a different user. The vault tracks the historical voting power of each address and, when asked for voting power, searches the historical record of that address’ voting power at the time when the vote was proposed.

#### **The Vesting Vault**

The vesting vault has the same functionality that the locking vault has, but for vesting. This vault allows locked / vesting positions to still have voting power in the governance system and does so by using a defined multiplier for the vested tokens over unvested.

### Future Voting Vaults

In terms of future voting vaults, once the process for establishing logic for counting votes / providing voting power is complete, governance will vote to approve the method, and if successful, the integration is complete, and users can start voting!

**Some of the possible future voting vaults consist of:**

* **Compound/Aave Vault **— use tokens as collateral and/or earn interest while keeping voting power.
* **LP Vault **— get voting power while providing liquidity.
* **Ouroboros Vault **— deposit Element principal tokens to get more votes than your current balance.
* **Identity Verified Vault **— verify your digital identity as a unique person to get voting power.
* **L2-L1 Synthesis Vault — **L2 posts balance tree hashes and L1 votes using the Merkel balance proof of L2.

If you have any other creative ideas for future voting vaults, let us know in [Discord](https://discord.com/invite/8JnDyXJJWh)!
