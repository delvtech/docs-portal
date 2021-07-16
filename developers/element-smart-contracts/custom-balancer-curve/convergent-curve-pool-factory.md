# Convergent Curve Pool Factory

* **Contract Name:** ConvergentCurvePoolFactory.sol
* **Type/Category:** Factory
* \*\*\*\*[**Associated System Diagram**](https://github.com/element-fi/elf-contracts/wiki/Core-Contract-Diagrams#convergentcurvepool)**:** n/a 
* **Contract Source:** [https://github.com/element-fi/elf-contracts/blob/main/contracts/factories/ConvergentPoolFactory.sol](https://github.com/element-fi/elf-contracts/blob/main/contracts/factories/ConvergentPoolFactory.sol)

## 1. Introduction \(Summary\)

The Convergent Curve pool factory deploys convergent curve pools. It also stores the address which can collect Element protocol fees from the pool and the Element protocol fee.

## 2. Contract Details

### **Key Functionality:**

* `create`: Deploys a new pool contract and registers it with Balancer V2's vault contract. The Convergent Pool Factory must be given permission by Balancer before being able to register pools. 
* `setGovFee`: Changes the percent of swap fees that go to the Element protocol.
* `setGov`: Changes the address which can collect element protocol fees.

**Storage:** This contract stores the percent fee the Element protocol collects of swaps and the address which can collect that fee from pools.

## 3. Key Mechanisms & Concepts

When called the contract will deploy a pool. When that deployment function is called the new pool contract will be registered with Balancer V2. Anyone can deploy a pool from this contract but only privileged addresses can reset the fee or where it goes. It's important to note that the fee switch and collection address changes only affect pools that are deployed in the future, and not any currently existing pools.

## 4. Gotchas \(Potential source of user error\)

Pool deployment can fail if the Element protocol fee is set too high or other sanity checks fail in the constructor of the pool.

## 5. Failure Modes \(Bounds on Operating Conditions & External Risk Factors\)

This deployer is locked to Balancer V2 and so becomes non-operational if Balancer V2 is not operational.

