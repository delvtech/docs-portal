# Core Protocol Contracts

The Core Protocol contracts allow the locking and tokenization of yield-bearing positions for fixed periods of time (terms). They define an abstract interface that allows developers to plug in various different integration contracts to generate yield. The focus of these contracts is simplicity, gas efficiency, and easy integration.&#x20;

**The below-listed contracts are the core protocol contracts of the Element Protocol:‌**

* **Wrapped Position: **The Wrapped Position tokenizes deposits in another protocol and defines the standardized external interface for integration contracts.
* **Tranche: **The Tranche contract is where Principal and Yield tokens are created by locking underlying tokens, and is unique for each expiration time and protocol integration pair.&#x20;
* **Tranche Factory: **The Tranche Factory uses a specialized deployment method to create unique predictable address tranches.
* **Interest Token: **The Interest Token is an ERC20 that is redeemable for yield in a specific tranche, it is more commonly referred to as Yield Token.
* **User Proxy: **The User Proxy is a contract that manages interactions with the protocol on behalf of users and holds allowances for them.
