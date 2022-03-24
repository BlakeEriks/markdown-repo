# Solidity

## Function Modifiers

These control when and where a function inside of a contract can be called from.

* **private** - only callable from other functions inside the contract.
* **internal** - only callable by contracts which inherit from this one
* **external** - only be called outside the contract
* **public** - can be called anywhere, internally and externally.

## State Modifiers

These functions tell us how the function interacts with the Blockchain.

* **view** - running this function will not change or save any data
* **pure** - same as view, except it also doesn't read any data from the blockchain

Both of these functions don't cost any gas to call if they are called from outside the contract (but do cost gas if called internally by another function)

## Custom Modifiers

Custom logic to determine how they define a function, ex onlyOwner, or aboveLevel.