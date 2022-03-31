# Custom Balancer Curve

Element has developed a custom trading curve algorithm that can be deployed on [Balancer V2](https://github.com/balancer-labs/balancer-v2-monorepo) that reduces slippage and impermanent loss. The Element protocol enables efficient trading of principal tokens with this custom AMM design, which is an implementation of the Yield Space AMM with small tweaks.&#x20;

**The below-listed contracts are the custom Balancer Curve contracts of the Element Protocol:‌**

* **Convergent Curve Pool:** The convergent curve pool contract is an implementation of a Balancer pool that provides quotes for trades when called by the Balancer V2 vault. It cannot be interacted with directly.
* **Convergent Curve Pool Factory:** Deploys a convergent curve pool for a principal token underlying pair.
