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

The above method for randomness is vulnerable to attack by a dishonest node. The best way to prevent this is to use an oracle outside of the blockchain.

## Tokens

A token on Ethereum is just a smart contract that follows some common rules. ERC20 defines a standard set of functions that all other tokens share. This allows all tokens which implement this set of functions to be interacted with in the same way. This makes it easy for exchanges to onboard with new tokens. 

There's another standard, ERC721, that doesn't make all tokens equal. It does provide logic for auction and escrow logic tho. Using this standard gives us the benefit of not having to roll out our own trading logic.

The ERC721 Standard:
```js
contract ERC721 {
  event Transfer(address indexed _from, address indexed _to, uint256 indexed _tokenId);
  event Approval(address indexed _owner, address indexed _approved, uint256 indexed _tokenId);

  function balanceOf(address _owner) external view returns (uint256);
  function ownerOf(uint256 _tokenId) external view returns (address);
  function transferFrom(address _from, address _to, uint256 _tokenId) external payable;
  function approve(address _approved, uint256 _tokenId) external payable;
}
```

### balanceOf Function

This function simply takes an **address** and returns how many tokens that **address** owns

### ownerOf Function

This function takes a token ID and returns the address of whoever owns it.