# Optimistic Grants

* **Contract Name: OptimisticGrants.sol**
* **Type/Category:** Grants/Governance
* **Contract Source:**[https://github.com/delvtech/council/blob/main/contracts/features/OptimisticGrants.sol](https://github.com/delvtech/council/blob/main/contracts/features/OptimisticGrants.sol)

## **1. Introduction (Summary)**

This contract allows for grants to be made to contributors of the Element protocol with less overhead than other grant programs. When the grant is allocated, it contains an expiration date, and if not removed before then, it is assumed the grantee did what was expected, and they are allowed to withdraw.

## **2. Contract Details**

**Key Functionalities:**

* Allow the owner to create and remove grants.
* Allows grantees to claim grants after they have completed their work.

**Storage:**

* A mapping tracking grants.
* An address authorized to create and remove grants.
* A tracker of the number of tokens the contract holds.

## **3. Key Mechanisms & Concepts**

The optimistic grants program can be run directly by a DAO-wide governance vote, but it is more likely that it will handle grants allocated by a permissioned group like the GSC. Unlike other grants programs, the optimistic grants smart contract sets a schedule so that, after the grant period is up, the grantee can claim the grant. The default assumption of someone receiving an optimistic grant is that they will perform as the grant would indicate. Only in the case of non-performance, the grant is removed by the funding body.

## **4. Gotchas (Potential source of user error)**

* The authorized grant address must fund the contract via the deposit method
* The grant contract tracks solvency, so it must be funded before grants are created.
* Funds directly transferred to this contract may not be recoverable.
