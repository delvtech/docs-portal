# Governance Glossary

### Delegation

ELFI holders can delegate their voting power/voting rights to an address. Delegation can be given to one address at a time, including the holder’s own address. Note that delegation does not lock tokens; it simply adds votes to the chosen delegation address.

### Proposals

**Element Governance Proposals (EGPs):** EGPs are standardized proposals subject to voting that (once enacted) regulate and define the behavior of the Element DAO's Governance system and the Element Protocol.

### **Types of Proposals (EGPs):**

* **Protocol (Executable) Proposal**: This category of proposals should be used when implementation involves the execution of one or more smart contract operations by accounts controlled by the Element DAO. A Protocol proposal is a type of proposal that is executed by the governance contract through timelock. It can replace the governance contract or perform an almost infinite range of other on-chain actions. In order to create a proposal on-chain, the proposer must have the voting power of 55 thousand or more.\

* **DAO (Social) Proposal:** This category of proposals should be used when a community member makes a request of the DAO that cannot be executed or enforced on-chain.

### Voting

* **ELFI (Governance Token):** The amount of ELFI you own in the system. Your ELFI can be delegated to give someone voting power, where 1 ELFI = +1 Voting Power.\

* **Quorum**: The purpose of quorum is to ensure that the only measures that pass have adequate voter participation. In order for a vote to pass, a certain percentage of voting power must vote in the affirmative. More specifically, for a proposal to succeed, a minimum of 1.1 million voting power (9.1% of the total) must participate in the vote. The quorum value may change as governance begins to understand participation rates but all changes to quorum requirements must be ratified by the governance community.\

* **Voting Power:** All voting power allocated to you from voting vaults and delegated ELFI.\

* **Voting Vaults:** Voting Vaults provide the ability to assign voting power to specific types of tokens/positions. The result is beautiful — governance users can maximize capital efficiency while maintaining the ability to delegate or vote when the time comes. Voting vaults are designed to be upgraded, allowing for voting vault logic to be updated by governance and to avoid the pains that come with governance upgrade migrations.\
  \
  The creation of a voting vault begins with defining a strategy for counting votes / providing voting power. Once the logic has been established, governance will vote to approve the method, and if successful, the integration is complete, and users can start voting.\

* **Locking Vault:** The locking vault allows users to deposit their tokens into a contract in exchange for voting power, which can also be delegated to a different user. The vault tracks the historical voting power of each address and, when asked for voting power, searches the historical record of that address’ voting power at the time when the vote was proposed.\

* **Vesting Vault:** The vesting vault has the same functionality that the locking vault has, but for vesting. This vault allows locked / vesting positions to still have voting power in the governance system and does so by using a defined multiplier for the vested tokens over unvested.\

* **Governance Steering Council (GSC) Vault:** The GSC vault enables a different mode of governance than the rest of the voting vaults. It gives one vote to each member of a council. When attached to a core voting contract, it enables the council members to vote on proposals and execute them only with agreement from the council. The council is selected by a continuous election of governance power in another core voting system.\

* **Voting Period (Snapshot)**: The total voting period in which votes can be cast. Proposals on Snapshot have a 5 day voting period.\

* **Voting Period (On-chain):** The total voting period in which votes can be cast. \[Minimum voting period]\[extra voting period] is the layout of the total time for voting. On-chain proposals have an \~8 day voting period.\

* **Timelock**: The timelock is a speed bump for calls. It requires calls to wait for a period before they can be executed. After a call is registered, the call can be removed during the waiting period, and an authorized address can extend the waiting period only once.

