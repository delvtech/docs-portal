# Yield Tokens

The redemption value for a YT at the end of the defined term will be the average yield it has earned over the course of the term on the principal it represents.

**Example**

* eY:yETH represents the yield gained on an ETH Yearn position listed at 25% APY.
* 1 eY:yETH reflects the yield gained from 1 ETH principal.
* The eY:yETH is under a 1-year term.
* If the Yearn position maintains 25% APY for the entire year, eY:yETH is redeemable for 0.25 ETH.

![](https://i.imgur.com/SixqVVj.jpg)

However, by definition, no variable yield position on the market maintains its listed yield rate (APY). The APYs constantly fluctuate. This implies that the real redeemable yield at the end of the year is unknown.

**Notes:**&#x20;

* The use of 1-year terms displayed in the above examples is purely for simplicity. The Element protocol will initially allow users to mint both 3-month and 6-month terms.
* The combined yield token and principal token redemption at maturity will not exceed the value of the yield asset in the Ethereum contracts. The yield token is only redeemable for the differential in value of the underlying yield asset from the original principal. It does not transfer financial risk associated with a future change in any such value or level without also conveying a current or future direct or indirect ownership interest in an asset (including any enterprise or investment pool) or liability that incorporates the financial risk so transferred. All growth or changes are denominated in the original asset.
