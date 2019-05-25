---
title: Getting started with Ethereum development
layout: post
---

This is a follow up post to Ethereum technical primer where the basic concepts of Blockchain and Ethereum are explained. In this post we shall discuss in detail how to set up a development environment and how to build Dapps(Distributed Apps) using Ethereum smart contracts.

## Installing Dev tools

### Installing testrpc

The easiest way to get started with setting up a local client is using [testrpc](https://github.com/ethereumjs/testrpc). Testrpc simulates a client in your local machine where you can deploy and test your smart contracts. You can install it using the command

```
npm install -g ethereumjs-testrpc
```


### Installing Truffle

[Truffle](https://github.com/trufflesuite/truffle) is a Ethereum development framework. It allows us to easily develop smart contracts and deploy it in the network(testrpc). It also allows us to write tests for our smart contracts. I highly encourage you to go through the [truffle documentation](http://truffleframework.com/docs/) to understand it better. You can install truffle using the below command.

    npm install -g truffle

These two should be sufficient for us to get started.

## Building a Dapp

Now we can go ahead and start building a dapp. The example I will be showing is a small stock exchange where we can buy and sell stocks.

### Creating project in Truffle

Create a new directory StockExchange and create a new truffle project inside it. You can create a new project in truffle using the command below

    truffle init webpack

This will create a new project with the following structure:

* ```app/``` - This directory contains the Frontend and UI(HTML, JS and CSS files).

* ```contracts/``` - This is a directory to put all your smart contracts.

* ```migrations/``` - Contains migration and deployment files — we can deploy the smart contract and specify its initial state here.

* ```test/``` - Test files for testing your application and contracts.

* ```truffle.js``` - your main Truffle configuration file.

* ```webpack.config.js``` - You can configure your webpack settings.

### Creating smart contract

We can create smart contracts using [Solidity](https://solidity.readthedocs.io/en/develop/). Solidity is an high level language designed to create smart contracts on the Ethereum Virtual Machine(EVM). We can create a smart contract for StockExchange step by step.

1. Create a sol file named **StockExchange.sol** in the **contracts** folder in your project.

1. Copy the contents from the below gist and add it to the file.

```solidity
pragma solidity ^0.4.2;

contract StockExchange {

	mapping (address => uint) balances;
	uint holdings;

	event Transaction(string _type, address indexed user);

	function StockExchange() {
		holdings = 10000;
	}

	function buy() payable{
		if(msg.value == 1 ether){
			balances[msg.sender] += 1;
			holdings -= 1;
			Transaction("Buy",msg.sender);
		}
	}

	function sell(){
		balances[msg.sender] -= 1;
		holdings += 1;
		msg.sender.transfer(1 ether);
		Transaction("Sell",msg.sender);
	}

	function getBalance(address addr) returns(uint) {
		return balances[addr];
	}

	function getHoldings() returns(uint) {
		return holdings;
	}
}
```

### Dissecting the smart contract

    pragma solidity ^0.4.2;

**pragma** is used to specify the solidity version using which the smart contract compiles. This is to avoid backward compatibility issues.

    mapping (address => uint) balances;

**mapping** is similar to **hashmap**where we can hold a key value pair. Here we use it to hold the balance for each account.

    uint holdings;

**Holdings** is used to denote the stocks held by the company. uint denotes unsigned integer.

    event Transaction(string _type, address indexed user);

Events are used to publish a event from the smart contract to the outside world. Events can be listened from the Dapps , as soon as an event is fired the listener will get the contents emitted from the event. Here we emit a **Transaction event **with either “Buy” or “Sell” to indicate the type of Transaction and the address of the user who performed the transaction. The indexed keyword allows us to filter the events on the listener side.

    function StockExchange() {
      holdings = 10000;
    }

StockExchange() is a **constructor** and we initialize holding with 10000 stocks.

    function buy() payable{
      if(msg.value == 1 ether){
       balances[msg.sender] += 1;
       holdings -= 1;
       Transaction("Buy",msg.sender);
      }
     }

Buy is a method which can be executed from Dapp. Notice the **payable** keyword in the function. It allows the method to **receive ether**. We can get who initiated the transaction using msg.sender. We can check how much ether is sent using msg.value. The other business logic is self explanatory and after the buy is completed we generate a **Transaction event**of type**“Buy”.**

    msg.sender.transfer(1 ether);

You may have noticed the above statement in **sell** method. This is used to send Ether directly to the sender from the smart contract.

Now that our smart contract is done, we need to modify the migration file to deploy this contract to the network.

### Modifying the migration file

Go to migrations/deploy_contracts.js. Clear whatever it has and add the following code to it.

    var StockExchange = artifacts.require("./StockExchange.sol");

    module.exports = function(deployer) {
      deployer.deploy(StockExchange);
    };

This is used to deploy the smart contract we created to the network(testrpc).

### Compiling and deploying the smart contract

1. Start running testrpc by typing testrpc in the terminal

1. You can compile the smart contract using truffle compile.

1. You can deploy the smart contract using truffle migrate. This executes the migration script we wrote above.

Now that our backend is ready we can go ahead and create our interactions and UI.

### Interacting with smart contracts

Go to app/javascripts/app.js and copy paste the contents of [this gist](https://gist.github.com/karthickpdy/f35fad39daf5c035fd04b254068401f1). We can discuss the major parts of the gist below.

1. We use Web3 library to interact with the smart contracts we created.

1. truffle-contract provides us methods to access the contracts which are deployed on the network.

1. Web3.eth.getAccounts gets us a list of all accounts created by testrpc. We can use first account as default account for our transactions.

1. We then get the deployed stock exchange instance and call the **buy transaction**on it. Anything that modifies the blockchain is called a **transaction**and it requires **gas**for its execution. Our buy function modifies the blockchain and thus its a transaction.
```js
    StockExchange.deployed().then(function(instance) {
          meta = instance;
          return meta.buy({from: account,value: web3.toWei(1, "ether")});
        })
```

5. You may have noticed that the function getBalance has been called differently. This is because getBalance **does not modify the blockchain** and hence it is considered as a **call**. This does **not cost gas**for its execution and thus it is denoted by the keyword call to differentiate from the transaction.

    StockExchange.deployed().then(function(instance) {
       meta = instance;
       return meta.getBalance.call(account, {from: account});
     })

6. We can use the default web3 method web3.eth.getBalance to get the ether balance of any address. Here we are using it to check the ether balance of the account doing the transaction.

7. As we already discussed our smart contract emits Transaction Event. We can listen to that event and display it in the UI using watch. You can see that we are listening to only the current accounts events using the **user filter.** This is possible because of indexing the user field in our smart contract.
```js
    StockExchange.deployed().then(function(instance) {
      instance.Transaction({user: account},{fromBlock: "latest",toBlock: 'latest'}).watch(function(err,result){
            self.setStatus(result.args._type+" - "+ result.args.user);
          });
      });
```
### Creating the UI

Now that the interaction part is done go to app/index.html and paste this gist.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Stock Exchange - Truffle Webpack Demo w/ Frontend</title>
  <link href='https://fonts.googleapis.com/css?family=Open+Sans:400,700' rel='stylesheet' type='text/css'>
  <script src="./app.js"></script>
</head>
<body>
  <h1>Stock Exchange</h1>  
  <h3>Company Stock Balance - <span class="black"><span id="holdingBalance"></h3>
  <h3>Account Stock Balance - <span class="black"><span id="balance"></h3>
  <h3>Account Ether Balance - <span class="black"><span id="etherBalance"></h3>
  
  
  <button id="buy" onclick="App.buy()">Buy</button>
  <button id="sell" onclick="App.sell()">Sell</button>
  <br><br>
  <h3>Latest Transaction</h3><span id="status"></span>
  
</body>
</html>
```

### Running the Dapp

Now we are all set to run and test our Dapp. Use the command npm run dev to start the server. It runs by default at localhost:8081. If you did everything correctly the output should be something like below.

![](https://cdn-images-1.medium.com/max/2000/1*CYhKDrOvFQr6ZzPsQkLlzg.gif)

For the curious, the decimal points in Ether balance is changing because of the gas usage for every transaction. The complete code is provided [here](https://github.com/karthickpdy/EthereumStockExchange). Feel free to play around with it. Hope the tutorial was useful and you learnt something from it. Cheers!

*If you liked this story, feel free to reach out to me at [http://karthickpdy.me/](http://karthickpdy.me/).*