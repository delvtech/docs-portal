---
description: >-
  After a proposal has been created on-chain it is subject to a Timelock
  Duration, Voting Periods, and Quorums. The initial governance (GSC, voting,
  delegation, etc) parameters can be found below.
---

# On-chain Voting Information

**Important Note:** All parameters described below may be changed by the governance community through a proposal and vote.

### **Governance Parameters**

| Parameter                      | Short Description                                                                                                                                                                                                                                                     | Value / Voting Power    | % of Total Voting Power  |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- | ------------------------ |
| Quorum                         | The required minimum number of voting power in support of a proposal for it to succeed.                                                                                                                                                                               | 1.1 million             | 1.1 million              |
| Proposal threshold             | The amount of voting power needed to submit a governance proposal on-chain.                                                                                                                                                                                           | 55 thousand             | 0.45% (1/20th of Quorum) |
| Timelock Duration              | The timelock is a speed bump for calls. It requires calls to wait for a defined period before they can be executed. After a call is registered, the call can be removed during the waiting period, and an authorized address can extend the waiting period only once. | 604800 seconds          | N/a                      |
| Voting Period                  | The total voting period in which votes can be cast. \[Minimum voting period]\[extra voting period] is the layout of the total time for voting.                                                                                                                        | 51968 blocks (\~8 days) |                          |
| Minimum Voting Period          | The minimum time before a vote can be executed.                                                                                                                                                                                                                       | 19488 blocks (\~3 days) | N/a                      |
| Extra Voting Period            | The time beyond the minimum time period in which votes can be cast.                                                                                                                                                                                                   | 32480 blocks (\~5 days) | N/a                      |
| Vesting Vault Token Multiplier | The multiplier for voting power on the vesting vault. The vesting vault allows locked / vesting positions to still have voting power in the governance system and does so by using a defined multiplier for the vested tokens over unvested.                          | 5%                      | N/a                      |

### **GSC-Only Parameters**

| Parameter                | Short Description                                                                                                                                                                        | Value        | % of Total Voting Power  |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------------------ |
| GSC Proposal Threshold   | The amount of GSC members needed to propose a GSC vote on-chain.                                                                                                                         | 1            | Undetermined             |
| GSC Delegation Threshold | A threshold of delegated voting power, giving delegates a seat on the GSC. This comes with additional governance powers within the system, and as a result, additional responsibilities. | 110 thousand | 0.90% (1/10th of Quorum) |
| GSC Quorum               | The required minimum number of GSC members needed to support a proposal for it to succeed.                                                                                               | 3            | N/a                      |





