---
description: A list of words and terms relating to the Element Protocol
---

# Glossary

The wording used in some of our documents may be unfamiliar to our readers. Some of the more commonly used terms are listed below to help with your understanding of the Element Protocol.

If you have additional questions regarding some of the documentation's explanations, please join our [Element community Discord](https://element.fi/discord).

| Term                              | Description                                                                                                                                                                                                                                                                                                                                                |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Principal Tokens (PTs)**        | The token representing the user's deposit value into the Element Protocol. These tokens are redeemable 1-for-1 for the underlying asset at maturity.                                                                                                                                                                                                       |
| **Yield Tokens (YTs)**            | The token representing the variable yield gain over the term period for the deposited underlying asset.                                                                                                                                                                                                                                                    |
| **Principal Reserves**            | The number of PTs staked in a pool pairing of the base asset and the PT. For example, the number of eP:yETH staked in the pool pairing of ETH / eP:yETH.                                                                                                                                                                                                   |
| **Base Asset**                    | The asset deposited into the Element Protocol (BTC, ETH, USDC, or DAI).                                                                                                                                                                                                                                                                                    |
| **Base Asset Reserves**           | The number of base assets staked in a pool pairing of the base asset with the PTs of said base asset. For example, the number of ETH staked in the pool pairing of ETH / eP:yETH.                                                                                                                                                                          |
| **Time Stretch Parameter**        | A parameter used in the trading curve that affects the price discoverability, fees, and staking ratio of the base asset to PTs.                                                                                                                                                                                                                            |
| **Annual Percentage Yield (APY)** | <p></p><p>Annual Percentage Yield is a time-based measurement of the Return On Investment (ROI) on an asset.</p><ul><li>For example, $100 invested at 5% APY would yield $105 after one year, if there is no compounding of any yield earned on that $100 through the year. Assuming a static APY rate, the Monthly ROI would be 0.41%.</li></ul>          |
| **Target APY**                    | The User's targeted Annual Percentage Yield.                                                                                                                                                                                                                                                                                                               |
| **Term**                          | A duration of time in which a user's assets are generating yield and deposited in the Element Protocol.                                                                                                                                                                                                                                                    |
| **Term Length**                   | The duration in which the user chooses to have their asset deposited in the Element Protocol, generating yield.                                                                                                                                                                                                                                            |
| **Vault**                         | A generic term for a yield-bearing asset.                                                                                                                                                                                                                                                                                                                  |
| **yVault**                        |  A programmatically adjusted lending aggregator, arbitrageur, and optimized yield generator ([reference](https://docs.yearn.finance/defi-glossary#yvault)).                                                                                                                                                                                                |
| **Automated Market Maker (AMM)**  | An AMM is a system that provides liquidity to the exchange it operates in through automated trading.                                                                                                                                                                                                                                                       |
|  **LP Tokens**                    | Tokens representing a user's liquidity position in an AMM.                                                                                                                                                                                                                                                                                                 |
| **Impermanent Loss (IL)**         | A loss that occurs when the value of the deposit asset is less compared to when they were deposited. In short, Impermanent loss is the difference between holding tokens in an AMM and holding them in your wallet. It occurs when the price of the tokens inside an AMM diverges in any direction. The more divergence, the greater the impermanent loss. |
| **Slippage**                      | The amount the price moves in a trading pair between when a transaction is submitted and when it is executed.                                                                                                                                                                                                                                              |
| **Yield Token Compounding**       | Depositing in a yield position and selling the principal to re-deposit, increasing exposure to yield. This is done multiple times, selling and re-depositing, and allows for leveraging into the yield at many multiples of the initial capital.                                                                                                           |