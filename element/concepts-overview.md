---
description: The Core Concepts of the Element Protocol
---

# Concepts Overview

### The Core Construct

The Element Protocol, at its core, works by enabling users via the Ethereum contracts to split the base asset (ETH, BTC, USDC, DAI) of yield generating positions, such as a Yearn vault or an ETH2 validator, into two separate, fungible tokens: the Principal Token (PT), and the Yield Token (YT). One token represents the value of the base principal (called the Principal Token), and one token represents the variable interest gained from the yield generating protocol (called the Yield Token).

![](https://i.imgur.com/6MuPE9S.png)

### Creating a Fixed-Rate Market

The two token split enables a wider degree of capital efficiency due to the secondary market available to trade these different components.

If a user opts to exit out of their base deposit position and maintain exposure to the variable interest earned by that base deposit, they may choose to sell their Principal Tokens in the AMM.

However, because the principal tokens are not redeemable until the term period is over, the principal tokens will naturally trade a discount relative to the underlying asset. The discounted rate, when purchased, determines a fixed rate of return as the principal token eventually converges to a 1:1 value to the underlying asset.

![](https://i.imgur.com/ogzNSjD.jpg)

Discounted assets allow users who are risk-averse to take on a safe guaranteed investment strategy without having to worry about the fluctuations of the variable interest market.

### Variable Interest Flexibility

With the Yield Tokens being liquid and tradable, users have the ability to take higher exposure to variable interest. A yield token for a 20% APY on 1 ETH will pay out 0.2 ETH annually. A user can opt to purchase a large sum of yield tokens before maturity and earn the remaining variable interest accrued during that term period.

By performing this action, the user facilitates exit liquidity for a seller to recognize their gains in the form of current accumulated yield.

![](https://i.imgur.com/GybzLUJ.jpg)

A user who wants to utilize the entire value of their capital towards variable interest, can do so and gain a very high return if the average APY of the vault utilized stays consistent.
