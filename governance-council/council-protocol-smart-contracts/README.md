# Council Protocol Smart Contracts

## Introduction

Council is a decentralized governance system that allows a community to manage a DAO. The governance system is designed to enable flexibility, improvements, and experimentation while successfully maintaining the security and robustness of the governed protocol.

Council is inspired by and extends several forerunners in the DAO governance space including MakerDAO's governance model and the Compound Governor contracts. Like these systems, it is a fully on-chain voting architecture that coordinates the process of making permissioned smart contract calls from privileged addresses.

**Council contains several architectural choices which make it a distinct new primitive in the decentralized governance space:**

* Council does not have a single security threshold to make a call, instead, various actions can be given different security threshold requirements.
* Council abstracts the vote allocation process for assigning voting power away from the actual voting process meaning that multiple complex vote allocation systems can run in parallel in the contracts.
* By default, Council ships with a Governance Steering Council (GSC) enabled which can be assigned different powers than the core voting system. Together, these features allow a wide range of voting processes and security procedures can be seamlessly integrated into one governance system.

For more details on the key features of the Council governance system, check out the below conference presentations:&#x20;

{% embed url="https://vimeo.com/637564907" %}

{% embed url="https://www.youtube.com/watch?v=wZj9HgwXel4" %}

## Architecture Overview

![To learn more about the technical architecture of Council, read this blog post.&#x20;
](../../.gitbook/assets/council-arch.png)

### Resources

* Introduction to Element's Governance System [blog post](https://medium.com/element-finance/an-introduction-to-elements-governance-model-efea13d1c7ee)
* [Github Repository ](https://github.com/element-fi/council)
* To learn more about the technical architecture of Council, read [this](https://medium.com/element-finance/element-governance-a-technical-architecture-overview-2d0f72bd278a) blog post. \
