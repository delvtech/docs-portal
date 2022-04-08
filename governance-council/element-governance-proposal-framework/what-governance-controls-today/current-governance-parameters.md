# Current Governance Parameters

### **General Governance**

* **Quorum:** The required minimum number of voting power in support of a proposal for it to succeed (this value is fixed and not a percentage of total voting power).
* **Timelock Duration:** The timelock is a speed bump for calls. It requires calls to wait for a defined period before they can be executed. After a call is registered, the call can be removed during the waiting period, and an authorized address can extend the waiting period only once.
* **Voting Period:** The total voting period in which votes can be cast. \[Minimum voting period]\[extra voting period] is the layout of the total time for voting.
* **Minimum Voting Period:** The minimum voting time before a vote can be executed.
* **Extra Voting Period:** The remaining time beyond the minimum voting period in which votes can be cast.
* **Vesting Vault Token Multiplier:** The vesting vault contract is used to set up long-term grants for core contributors to the Element ecosystem. It is also a voting vault so that community members can vote with vested but unclaimed tokens and unvested tokens. The **multiplier** for voting power on the vesting vault allows locked / vesting positions to still have voting power in the governance system and does so by using a defined multiplier for the vested tokens over unvested.
* **Proposal Threshold:** The amount of voting power needed to submit a governance proposal on-chain.

### **GSC Parameters**

* **GSC Delegation Threshold:** A threshold of delegated voting power, giving delegates a seat on the GSC. This comes with additional governance powers within the system, and as a result, additional responsibilities.
* **GSC Quorum:** The required minimum number of GSC members needed to support a proposal for it to succeed.
* **GSC Proposal Threshold:** The amount of GSC members needed to propose a GSC vote on-chain.
