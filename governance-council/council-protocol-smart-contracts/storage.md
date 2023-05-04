# Storage

* **Contract Name:** Storage.sol
* **Type/Category:** Library
* **Contract Source:**[https://github.com/delvtech/council/blob/main/contracts/libraries/Storage.sol](https://github.com/delvtech/council/blob/main/contracts/libraries/Storage.sol)

## **1. Introduction (Summary)**

The Storage library is a utility library designed to be used with the simple proxy(link). As a library, it is inherited and extended by all of the logic contracts for proxies.

## **2. Contract Details**

There is a set of functions that allow the reading and setting of variables for every type of contract, indexed by their names. The name and type are hashed together to produce a unique storage location and then assembly is used to set the location of a returned storage structure. For low-level types \[address, uintX, bytesX] assembly does not have access to the slot, and custom structs \[Addresses, UintX, BytesX] are returned instead. The library also contains custom structs for commonly used packing pairs \[(uint128, uint128), (uint96, address)]. As a library, it does not have any storage itself, and only contains the ability to help other contracts layout their storage.

## **3. Key Mechanisms & Concepts**

* Upgradable proxies in Solidity are harder to use securely because the Solidity compiler gives each storage variable a fixed slot in storage, based on declaration order in the source code. This is why special care must be taken to avoid storage corruption on upgrades.
* This storage library is a way around that uses a hash of the variable name and variable type to assign storage locations, meaning they can be easily accessed across upgrades. They are also much harder to corrupt.

## **4. Gotchas (Potential source of user error)**

* Two variables of different types may share the same name, and so when loaded with different type functions, load different locations. Nevertheless, we do not encourage using two variables with the same name as it is bad practice.
* Due to the custom storage layout, other storage libraries should not be assumed to work with this library. We heavily discourage the usage of normal storage management and especially storage assembly simultaneously as this library.
* Do not allow external access to inputs that are provided as variable names when calling this library. We strongly encourage all variable names to be constant strings set on compile.
* Due to the pointer system of this contract memory, corruption can cause storage corruption. We strongly discourage interacting with memory assembly in conjunction with this contract and recommend modern versions of solidity.
* When using this library we recommend the code to be audited by an auditor with extensive low-level EVM experience.

## **5. Failure Modes (Bounds on Operating Conditions & External Risk Factors)**

* This contract can cause storage corruption if not used securely or due to cascading failures in other places.
