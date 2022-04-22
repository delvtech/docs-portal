# Simple Proxy

* **Contract Name:** SimpleProxy.sol
* **Type/Category:** Proxy
* \*\*Contract Source: \*\* [https://github.com/element-fi/council/blob/main/contracts/simpleProxy.sol](https://github.com/element-fi/council/blob/main/contracts/simpleProxy.sol)

## **1. Introduction (Summary)**

The simple proxy is used to make a contract upgradeable by splitting the state from the logic run by the smart contract. It is implemented in gas-efficient assembly and calls a changeable logic contract that runs the code in that contract using the storage of the proxy.

## **2. Contract Details**

The key functionalities of the smart contract are the ability to accept calls from users and run the code of another contract as if they had called it, and the ability to change which contract's logic is used. The simple proxy stores the address of the implementation and the address allowed to upgrade that implementation.

## **3. Key Mechanisms & Concepts**

The simple proxy's fallback function will take the data provided by the caller and forward that data as a delegate call to the implementation address, then propagate any return or error back to the caller. The fallback uses optimized assembly to achieve this efficiently. Since the proxy uses delegate call, the address of the proxy will have any state changes made in it, instead of in the address of the implementation. Therefore, if the implementation is changed, the new implementation will have access to the same storage. The only other function in the proxy allows a governance address to change the implementation address, which is called when the callback function executes.

## **4. Gotchas (Potential source of user error)**

* The governance and implementation address is normally stored in the contract so any logic contract must use the storage library to manage storage or will almost certainly corrupt storage.
* Function names 'upgradeProxy(address)' 'resetProxyOwner(address)' and their corresponding selectors cannot be used in logic contracts and are reserved for the proxy.

## **5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)**

* The governance address can make any change to the storage or usage of the proxy; therefore, upgradable contracts are only as secure as their governance mechanism. If governance is corrupted the whole contract is also corrupted.
