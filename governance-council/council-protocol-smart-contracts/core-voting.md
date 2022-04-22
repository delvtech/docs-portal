# Core Voting

* **Contract Name:** CoreVoting.sol
* **Type/Category:** Governance
* **Contract Source:** https://github.com/element-fi/council/blob/main/contracts/CoreVoting.sol

## 1. Introduction (Summary)

The core voting contract allows a voting process for those who have been allocated governance power. It allows them to select which calls are executed from the core voting contract address and does not make assumptions about how the voting power is allocated. Instead, it calls designated contracts that calculate how much voting power a user has for the voting contract. Calls can be executed at a variety of different security thresholds for various different external functionalities. The contracts which calculate votes for the core voting contract are called voting vaults, and the sum of what they indicate for a user at a timestamp is that user's voting power.

## 2. Contract Details

The core voting allows the proposal of a package of calls to be made from the core voting contract. Each of these calls corresponds to some action on the Ethereum blockchain. Each proposal must be proposed by either an authorized user \[Governance steering council] or by someone with sufficient voting power. Then, each of the users who have voting power can cast a vote for, against, or neutral on each proposal. If the proposal gains more votes than a security threshold, the proposal can then be executed after some minimum time, and before an expiration time. An authorized address can change all parameters of the voting contract. In a normal operation, that address is the timelock contract. The core voting contract stores a mapping containing previous proposals organized according to an id associated with each proposal, timelock address, minimum and maximum voting times. Also, the minimum power needed to propose a vote, a mapping that records custom quorums, a default quorum, and a listing of approved voting vaults.

## 3. Key Mechanisms & Concepts

The voting contract accepts in calldata a list of vaults in which the user may have voting power to calculate the voting power for a user, the core voting contract then checks that each vault in the list is approved, and calls them with the sender's address, timestamp, and optional extra data. The voting vault responds with a number of votes allocated to the user. To create a proposal the creator's voting power is checked and then the proposal is created by assigning the last unused proposal id to the new proposal, and storing its data into the proposals mapping. After the proposal is created, a user can vote on a proposal by indicating the proposal id they would like to vote on. Then, their voting power is calculated, and added to a running tally of the votes for yes, no, or abstain. Votes cannot be made on a proposal after a max time from proposal creation. If a proposal has more votes cast than the quorum threshold for the action/s being taken, and more yes votes than no votes, then the proposal can be executed. Proposal execution will fail if the proposal is past an expiration timestamp.

## 4. Gotchas (Potential source of user error)

* Votes can be changed or removed by calling the vote function again, with a new ballot to change them, or with an empty set of voting vaults to remove them.
* All actions in a proposal must succeed or the execution of that proposal will revert. Therefore, any proposal must be created without any calls that have a high probability to revert.
* Anyone can execute the transactions approved by the governance system, therefore, any bundle of transactions made should be vetted to not have exploitable downstream effects if sandwiched by an adversary.
* The quorum of a bundle of onchain actions is set as the maximum in that bundle, meaning that it should be vetted if the quorum is lowered. For an action it should be secure even if called multiple times in the same transactions or with other low quorum actions.

## 5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)

* Since the voting contract can change its own configuration it can put itself into a position where it is no longer functional by making improper changes to its own variables. There is no recovery mechanism for this format of bricking so the governance contract variable upgrades must be held to the highest security standards.
* The modular nature of the governance systems is designed to enable upgradeability. In the case of a component like a voting vault fails, it should be voted on to be removed from the governance contract. In a case where the core voting contract is out of date, it can change the core voting contract in the time lock and other permissioned contracts to replace itself.
