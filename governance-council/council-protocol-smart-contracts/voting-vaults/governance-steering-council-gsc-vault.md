# Governance Steering Council (GSC) Vault

* **Contract Name:** GSCVault.sol
* **Type/Category:** Voting Vault/Governance
* **Contract Source:**[https://github.com/element-fi/council/blob/main/contracts/vaults/GSCVault.sol](https://github.com/element-fi/council/blob/main/contracts/vaults/GSCVault.sol)

## **1. Introduction (Summary)**

The GSC vault enables a different mode of governance than the rest of the voting vaults. It gives one vote to each member of a council. When attached to a core voting contract, it enables the council members to vote on proposals and execute them only with agreement from the council. The council is selected by a continuous election of governance power in another core voting system.

## **2. Contract Details**

**Key Functionalities:**

* Allow anyone to join the governance steering council if they prove they meet a minimum voting power in the DAO.
* Allow anyone to kick a member if their voting power falls below a threshold.
* Give each member one vote after they have been on the council for a warmup period.

**Storage layout:**

* A mapping tracks who is a member and when they joined.
* An upgradable bound on how many votes are needed to join or remain on the council.
* An upgradable warmup period length.

## **3. Key Mechanisms & Concepts**

The Governance Steering Council (GSC) is designed to be a group of people who take on extra responsibility in the DAO and gain extra powers. To join, the members must maintain some minimum amount of voting power in the DAO. The members can vote on issues through a copy of the core voting contract \[which is not the same voting contract as in the primary DAO]. To maintain the list of the GSC members, we use a model where the prospective member should prove membership by proving they have enough voting power in the DAO. To remove a member, they are challenged. The voting vaults which initially contained their voting power are queried and, if they have not maintained enough power, they are removed.

## **4. Gotchas (Potential source of user error)**

* If there is a vault migration where the source of member voting power changes, they have to reprove their membership. This reproof does not cause another idle period before they can vote.
* Since the GSC vaults stores the data of the voting vaults, the member votes and queries them again on kick. The voting vaults of the DAO must enforce that a voting power query that previously didn’t revert does not start reverting. If that happens, members may become un-kickable.
* Some vaults require extra data, for example, to provide a Merkle proof or signature, in order to kick a member who joins using those vaults the kicker must provide valid data as well.

## **5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)**

* In the case of corruption or inaction by the GSC, the DAO can vote to vote on the GSC core voting contract and be given a high number of votes. Meaning that the decisions of the GSC can be overridden by the DAO via vote.
  * This also is a remediation path to many bugs in the GSC vault.
