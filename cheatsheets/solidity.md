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

### Payable modifier

A special modifier that allows a function to receive Ether. 

```js
contract OnlineStore {
  function buySomething() external payable {
    // Check to make sure 0.001 ether was sent to the function call:
    require(msg.value == 0.001 ether);
    // If so, some logic to transfer the digital item to the caller of the function:
    transferThing(msg.sender);
  }
}
```

Example usage

```js
// Assuming `OnlineStore` points to your contract on Ethereum:
OnlineStore.buySomething({from: web3.eth.defaultAccount, value: web3.utils.toWei(0.001)})
```

> Note: If a function is not marked payable and you try to send Ether to it as above, the function will reject your transaction.

## Transfer Function

After sending Ether to a contract is gets stored in the contracts Ethereum account & trapped there unless there is a function to withdraw it.

```js
contract GetPaid is Ownable {
  function withdraw() external onlyOwner {
    address payable _owner = address(uint160(owner()));
    _owner.transfer(address(this).balance);
  }
}
```

> We are using **owner()** and **onlyOwner** from the **Ownable** contract

## Randomness

The best source of randomness in Solidity is the **keccak256** hash function. 

```js
// Generate a random number between 1 and 100:
uint randNonce = 0;
uint random = uint(keccak256(abi.encodePacked(now, msg.sender, randNonce))) % 100;
randNonce++;
uint random2 = uint(keccak256(abi.encodePacked(now, msg.sender, randNonce))) % 100;
```

The above method for randomness is vulnerable to attack by a dishonest node. 