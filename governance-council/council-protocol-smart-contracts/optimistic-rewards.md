# Optimistic Rewards

* **Contract Name:** OptimisticRewards.sol
* **Type/Category:** Rewards/Governance
* **Contract Source:**[https://github.com/delvtech/council/blob/main/contracts/vaults/OptimisticRewards.sol](https://github.com/delvtech/council/blob/main/contracts/vaults/OptimisticRewards.sol)

## **1. Introduction (Summary)**

The Optimistic Rewards contract is a system for allocating rewards over time without writing new rewards smart contracts. It allows a proposer to propose a new set of rewards and then, after a review period, it is made official. During the review period, governance can reject the proposed rewards.

The name optimistic comes from the fact that the mechanism is a play on an optimistic rollup, where the fraud proofs are governance votes but, instead of L2 transactions, the updates are new rewards balances.

## **2. Contract Details**

**Key Functionalities:**

* The ability for addresses who have confirmed rewards to claim those rewards, or to claim them and then move them into the DAO to continue voting.
* The ability for addresses who have confirmed rewards but have not claimed them to vote using them as votes.
* A proposer can propose a new Merkle root encoding rewards.
* Governance can reject a new Merkle root encoding rewards.

**Storage layout:**

* A Merkle root containing confirmed rewards.
* A mapping of how many rewards each address has claimed.
* A proposed root and when it was proposed.
* A challenge period length.

## **3. Key Mechanisms & Concepts**

Rewards systems voted in DAOs are often complex mathematical formulas on how much incentive to give to taking actions in the protocol. Each of these mechanisms must often be encoded into smart contracts. Given the security risk of smart contracts and implementation complexity, this naturally limits what can be done with rewards, how complex they are, and how fast they can change or be implemented. The optimistic rewards paradigm is a way to move rewards calculation off-chain and alleviate those limitations. To accomplish this, a proposer address is selected by governance. The proposer runs a deterministic program that calculates rewards, and then submits this on-chain for review. Community members also run the rewards program and, if fraud is detected, they can submit a DAO vote to remove the proposer and block the rewards. Given an active community, there is no incentive for a malicious proposer to submit rewards.

## **4. Gotchas (Potential source of user error)**

* Rewards Merkle roots must contain unique accounts, they must be append-only, and the accounts must only increase in rewards allocated. The root tracks the total all-time rewards granted.

## **5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)**

* An engaged community of verifiers of rewards is required for this system to work. The DAO should consider allocating rewards to chain watchers to encourage this.
* The total tokens in this contract should be limited so that, if a bug or hack occurs, the risk is mitigated.
