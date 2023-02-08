---
description: Definitions for commonly-used terms accross Element's Council governance
---

# Glossary (Governance)

### Basic Concepts

**ELFI:** The governance token for the Element Protocol. Each ELFI token allows the owner to delegate 1 unit of Voting Power to any address, including their own address (self-delegation). You can see the amount of ELFI you own in the [governance dashboard](https://gov.element.fi/).

**Voting Power:** The basic unit of governance power used for voting on proposals, which determines whether they pass or fail. ELFI holders own Voting Power, which they can then delegate for it to be usable in governance. You can see the amount of Voting Power delegated to you in the [governance dashboard](https://gov.element.fi).

**Delegation**: ELFI holders can delegate their voting power/voting rights to an address. Delegation can be given to one address at a time, including the holder’s own address. Note that delegation does not lock tokens; it simply adds votes to the chosen delegation address. This allows ELFI holders' votes to be used in governance through their delegates, which reduces both the financial and mental cost of participating in governance for individual holders.

You can see your current delegate and other delegation-related information on the [governance delegate page](https://gov.element.fi/delegate).

**Proposal:** Formal request to make a change on how any part of the protocol works. This can include, but is not limited to: adding, deleting or updating smart contract code, changing the protocol's stated mission or vision, defining how to spend treasury assets, executing any kind of on-chain transaction, changing governance processes and parameters, among others. Users will decide on whether a proposal passes or fails by using their Voting Power.

You can see active and past proposals in the [governance proposals page](https://gov.element.fi/proposals).

**Voting Vaults:** Set of smart contracts that determine how voting power is counted in the system. Each voting vault can be programmed to measure any metric to distribute voting power. For example: one voting vault could assign 1 vote per ELFI deposited, another one could assign 0.05 votes per ELFI vested, while another could assign 1000 votes per successful governance proposal submitted by a user. This gives the system enough flexibility to evolve alongside the needs of the DAO.

**Governance Steering Council (GSC):** Group of delegates who have surpassed a pre-established threshold of delegated Voting Power -currently defined as 10% of quorum, or 110k votes- and have claimed this governance role. The GSC holds additional governance powers, as well as the additional responsibilities that come with them.&#x20;

The extent of the GSC's functions and permissions is to be decided by the DAO through a governance proposal. If a GSC member falls below the threshold of delegated voting for being a member, they'll also lose their additional powers.

### Proposals

**Element Governance Proposals (EGPs):** EGPs are standardized proposals subject to voting that (once enacted) regulate and define the behavior of the Element DAO's Governance system and the Element Protocol.

#### **Types of EGPs:**

* **Protocol (Executable) Proposal**: This category of proposals should be used when implementation involves the execution of one or more smart contract operations by accounts controlled by the Element DAO. A Protocol proposal is a type of proposal that is executed by the governance contract through timelock. It can replace the governance contract or perform an almost infinite range of other on-chain actions. In order to create a proposal on-chain, the proposer must have the voting power of 55 thousand or more.
* **DAO (Social) Proposal:** This category of proposals should be used when a community member makes a request of the DAO that cannot be executed or enforced on-chain.

### Voting

**Quorum**: Minimum amount of votes required for a proposal's voting results to be considered valid. The purpose of this quorum is to ensure that the only measures that pass have adequate voter participation. More specifically, for a proposal to succeed, a minimum of 1.1 million voting power (9.1% of total) must participate in the vote. The quorum value may change as governance begins to understand participation rates but all changes to quorum requirements must be ratified by the governance community.

**Voting Vaults:** Voting Vaults provide the ability to assign voting power to specific types of tokens/positions. The result is beautiful — governance users can maximize capital efficiency while maintaining the ability to delegate or vote when the time comes. Voting vaults are designed to be upgraded, allowing for voting vault logic to be updated by governance and to avoid the pains that come with governance upgrade migrations.

The creation of a voting vault begins with defining a strategy for counting votes / providing voting power. Once the logic has been established, governance will vote to approve the method, and if successful, the integration is complete, and users can start voting.

**Locking Vault:** The locking vault allows users to deposit their tokens into a contract in exchange for voting power, which can also be delegated to a different user. The vault tracks the historical voting power of each address and, when asked for voting power, searches the historical record of that address’ voting power at the time when the vote was proposed.

**Vesting Vault:** The vesting vault has the same functionality that the locking vault has, but for vesting. This vault allows locked / vesting positions to still have voting power in the governance system and does so by using a defined multiplier for the vested tokens over unvested. For example, vested tokens could count for 0.05 votes each while unvested tokens count for 1 vote each.

**Governance Steering Council (GSC) Vault:** The GSC vault enables a different mode of governance than the rest of the voting vaults. It gives one vote to each member of a council. When attached to a core voting contract, it enables the council members to vote on proposals and execute them only with agreement from the council. The council is selected by a continuous election of governance power in another core voting system.

**Voting on Protocol Proposals**: Users can vote for or against single proposals once they have voting rights delegated to their address. Votes can be cast while a proposal is in the “Active” state.... the proposal may be queued in the Timelock.

**Voting Period (Snapshot)**: The total voting period in which votes can be cast. Proposals on Snapshot have a 5 day voting period.

**Voting Period (On-chain):** The total voting period in which votes can be cast. \[Minimum voting period]\[extra voting period] is the layout of the total time for voting. On-chain proposals have an \~8 day voting period.

**Timelock**: The timelock is a speed bump for calls. It requires calls to wait for a period before they can be executed. After a call is registered, the call can be removed during the waiting period, and an authorized address can extend the waiting period only once.
