# Convergent Curve Pool

* **Contract Name:** ConvergentCurvePool
* **Type/Category:** Automated Market Maker
* **Contract Source:** [https://github.com/element-fi/elf-contracts/blob/main/contracts/ConvergentCurvePool.sol](https://github.com/element-fi/elf-contracts/blob/main/contracts/ConvergentCurvePool.sol)

## 1. Introduction (Summary)

The Convergent Curve Pool (CCP) is an implementation of an automated market maker (AMM) algorithm that allows two tokens that converge in price to be market-made more efficiently than standard options. Standard market makers either expect prices to change frequently and unpredictably as in [Uniswap](http://uniswap.org) or [Balancer's](http://balancer.finance) weighted pool, or they expect the prices to not change over time as in [Curve](http://curve.finance). The CCP market maker works for assets that approach the same price over time and is mathematically in between the current options. The code is an implementation of the Yield space [paper](https://yield.is/YieldSpace.pdf) with some additional modifications and is designed to be integrated with Balancer V2.

![](https://i.imgur.com/ZWvaimk.png)

### **Glossary**

* **Automated Market Maker (AMM):** a trading algorithm that both buys and sells in an asset pair to add liquidity to the market.
* **Liquidity:** the ability of market participants to quickly purchase or sell an asset on the market.
* **Slippage:** the difference between hypothetical asset price and the actual price a user gets.
* **Invariant:** a number that must stay constant or go up when a user makes a trade (eg. x\*y in Uniswap)
* **Curvature:** a mathematical property of a function that refers to how fast a function 'bends' or the rate at which it changes.

## 2. Contract Details

### **Key Functionality**&#x20;

* `onSwap`: This method allows a user to indicate the details of a trade which they would like to make and then indicates the result of this trade. The Balancer V2 vault is responsible for managing the pool balances and trades so will call this method when a user requests a trade and use the output to make the trade on behalf of the pool.
* `onPoolJoin/onPoolExit`: These functions are called by the Balancer V2 Vault when a liquidity provider wants to join or exit the pool. In `onJoin` the caller provides the max amounts of tokens they can input and the pool indicates how many are consumed by the call. In `onExit` the caller provides the minimum output they want to receive and the pool burns enough LP token from them to output that amount. Balancer V2's vault does all of the underlying token management based on the pool's outputs.
* `transfer/approve/transferFrom`: The convergent curve pool is an ERC20 which allows the direct transfer of liquidity positions and so contains all standard ERC20 methods.

**Storage:**

The contract stores LP balances and allowances plus other constants to enable ERC20 functionality such as name and symbol. The pool stores the collected trade fees that have not had Element or Balancer Protocol fees assessed. These are used in internal calculations and are stored in an 18 decimal fixed point. Additionally, the pool stores as constants several details of the pool such as the tokens, token decimals, swap fee, unit seconds, and Element percent fee.

## 3. Key Mechanisms & Concepts

The pool uses the invariant `$x^{1-t} + y^{1-t}$` as the trade invariant, where `$x, y$` are the reserves and `$t$` is the fraction of the period remaining. This formula adjusts the curvature of the trading curve as time flows and so may not support some features of standard AMM curves. Please exercise caution and do thorough mathematical analysis before editing or integrating with unprecedented ways.

The pool charges a fee on each swap which is paid to liquidity providers. This fee is equal to some percent of the implied yield if the tokens converge in price. For example, if you buy 110 ether bonds for 100 ether the implied yield is 110 - 100 = 10, if the fee is 10% you get charged X eth as a fee. This fee mechanism keeps the pool slippage low when the assets are closest in price.

The trade fees are split between the liquidity providers, the Balancer V2 protocol, and the Element protocol. Both the Balancer V2 and Element protocol fees start at 0% and are bound at 30%. Balancer V2 fees are deducted directly from the pool's holdings, but Element protocol fees are collected to minting LP tokens to an address.

## 4. Gotchas (Potential source of user error)

* The unit seconds parameter has complex effects on the pricing curve and should be closely analyzed before deploying a pool.
* All internal pool calculations are done in 18 point fixed format, but tokens are often in other formats \[USDC is 6 decimal, and WBTC is 8]. The storage variables which track collected fees are in 18 point fixed so if loaded and interpreted using the token decimals may be wrong.
* The pool uses a proportional method for join and exit, so does not support additions of a single token, unlike other Balancer pools.
* In Balancer V2 arrays of input, values must be provided in order of the numerical order of the token addresses. So users who call join or exit on the pool must also provide their balances in this order.
  * **For example:** If USDC has address 0x03 and eUSDC has address 0x02, and I wish to deposit 50 USDC and 75 eUSDC I must provide \[75, 50] not \[50, 75] with my call to join the pool.
* To set trade prices the pool uses 'virtual reserve logic' which adds the total supply of LP tokens to the supply of bond tokens before applying the invariant.

## 5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)

* If the tokens do not converge in the price for any reason by the expiration time the pool will become entirely composed of the token of lesser value. Due to this, the pool can only give a guarantee of security of funds equal to that of the riskiest pool token.
* Balancer V2 controls all LP and user funds in the pool so this contract inherits all of the smart contract risk and the failure modes of the Balancer V2 protocol.
