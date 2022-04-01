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

## Web3.js

Web3 JS is an api on top of JSON-RPC which allows us to communicate to the ethereum network using javascript.

## Metamask

Metamask is a browser extension for Chrome and Firefox allowing users to securely manage their ethereum accounts and private keys, as well as use these accounts to interact with websites that use web3.js. 

Check for metamask:

```js
window.addEventListener('load', function() {

  // Checking if Web3 has been injected by the browser (Mist/MetaMask)
  if (typeof web3 !== 'undefined') {
    // Use Mist/MetaMask's provider
    web3js = new Web3(web3.currentProvider);
  } else {
    // Handle the case where the user doesn't have web3. Probably
    // show them a message telling them to install Metamask in
    // order to use our app.
  }

  // Now you can start your app & access web3js freely:
  startApp()

})
```

Web3 needs two pieces of information to talk to your deployed contract. The **address** and the **ABI**.

The **address** is the identifier where the contract lives on the blockchain. The **ABI** stands for Application Binary Interface, and it represents the contracts public methods, indicating to Web3.js how the contract can be interacted with. 

### **Web3.js Contract Functions**

Web3.js provides two methods we can use to call functions on our contract - *call* and _send_.

**Call** is used for **view** and **pure** functions. It will only run on the local node, and won't create a new transaction on the blockchain. These functions are read-only, and don't change any state on the blockchain. The user won't be prompted to sign any transaction with MetaMask when these occur.

Here's an example:

```js
myContract.methods.myMethod(123).call()
```

**Send** will create a transaction and change data on the blockchain, thus charging gas. Calling **send** is required for any function not labeled as view or pure. Metamask will popup for the user when this is called, and prompt them to sign the transaction and pay for the gas fee.

Example:

```js
myContract.methods.myMethod(123).send()
```

Sending a transaction in web3.js requires a **from** address of who's calling the function (this becomes the msg.sender address in the contract). There will be a significant delay when sending a transaction, as we must wait for it to be included in a block on the blockchain.

**Send** has event listeners **receipt** (success) and **error**.

When calling **send**, you can optionally specify **gas** and **gasPrice** as the programmer, otherwise MetaMask will allow the user to specify these values.

Web3.js lets us listen for Solidity firing events that we write in our contract.

Example

```js
cryptoZombies.events.NewZombie()
.on("data", function(event) {
  let zombie = event.returnValues;
  // We can access this event's 3 return values on the `event.returnValues` object:
  console.log("A new zombie was born!", zombie.zombieId, zombie.name, zombie.dna);
}).on("error", console.error);
```

This will notify our user whenever ANY new zombie is created. What if we only wanted alerts when the current user created a new zombie.

In order to filter events, our Solidity contract would need to use the **indexed** keyword.

Example filter of indexed event
```js
// Use `filter` to only fire this code when `_to` equals `userAccount`
cryptoZombies.events.Transfer({ filter: { _to: userAccount } })
.on("data", function(event) {
  let data = event.returnValues;
  // The current user just received a zombie!
  // Do something here to update the UI to show it
}).on("error", console.error);
```

We can query for past events using getPastEvents, and use the filters **fromBlock** and **toBlock** to give Solidity a time range for the logs. Block refers to the block number. 

```js
cryptoZombies.getPastEvents("NewZombie", { fromBlock: 0, toBlock: "latest" })
.then(function(events) {
  // `events` is an array of `event` objects that we can iterate, like we did above
  // This code will get us a list of every zombie that was ever created
});
```

> This presents a use case of using events as a cheaper form of storage, as saving data to the blockchain is very expensive. Using events is much much cheaper in terms of gas. The tradeoff comes into play when considering events are not readable from inside the smart contract itself. If you wanted some data to be historically recorded on the blockchain, events are a good contender.