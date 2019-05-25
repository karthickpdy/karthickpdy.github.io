---
title: Technical primer to Ethereum
layout: post
---

I attended a talk on Ethereum few weeks back and was fascinated by the possibilities it provided and started exploring the ecosystem. It is a pretty nascent ecosystem that is catching up fast among the developer community. In this post I will explain the technology behind Ethereum so that we can get started with developing with Ethereum. This assumes you have technology background and basic understanding of blockchain so that we can discuss the Ethereum implementation.

## First things first

Blockchain provides a **de-centralized**, **peer to peer**  network where digital assets can be transferred from one peer to another. The major problem we face in a de-centralized network is who will verify the validity of all the **transactions**  taking place? The short answer is **everyone.** 

Imagine a document with some information . Each person in the network keeps a copy of the same document. If there is an update in the document, it is propagated across the network and everyone updates their own copy of the document. Lets say a new person comes with different content in the document, then all the others can verify their copy and detect that the new person is lying and kick him out of the network. This is basically how a blockchain works.

First we need to understand few basic terms to get started.

### Hash

We can use a cryptographic hash function(SHA256) to convert any string to its equivalent hash. The hash has two unique properties:

1. The hash produced has **one to one mapping** with the input string. The same input always produces the same unique hash and no other input can have the same hash.

1. Even a **small change** in the input string will lead to a **large change**  in the output hash and thus the input can be easily validated.

### Transaction

The process by which assets are moved from one party to another in the network is known as Transaction. All transactions are recorded and permanently stored.Lets say A wants to transfer 5 Ether to B. Then this is a transaction in the network.

### Block

Many transactions are combined together to form a block. Each block consists a unique **hash** which identifies it in the network. A block is chained to previous block using the hash of the previous block.

### Genesis Block

The initial block or state of the blockchain that is agreed upon by all the nodes in the network.

### Blockchain

As the transactions are added many blocks are created and then they are chained together using their hashes into blockchain network.

### Proof of work

A **proof of work**  is a piece of data which is difficult (costly, time-consuming) to produce but easy for others to verify and which satisfies certain requirements. When there is a transaction in the network, any node that tries to process the transaction should solve a cryptographic puzzle for it to be accepted to the block. This is known as proof of work. The work that is to be performed can be done only by trial and error and this has to be performed for any valid transaction in the network before it can become part of the blockchain.

### Mining

The process of processing a transaction and adding it to the block by carrying out the proof of work is known as mining. The miners(nodes) get the rewards of the transaction once the transaction is accepted as part of the blockchain.

### Merkle Tree

A **Merkle tree**  is a tree in which every non-leaf node is labelled with the hash of the labels of its child nodes. We can verify that the data blocks received from other nodes are received undamaged and unaltered, and even to check that the other nodes do not lie and send fake blocks.

### Working

We can now move on to basic working of a blockchain.

1. Each node starts with genesis block and builds its way up to the “current state” of the blockchain. When it receives a new block each node verifies its hash and thus validates if its a valid block or not and keeps building the chain.

1. Once there is a transaction in the network, the miner mines it by generating the required proof of work. Then the miner adds it to his copy of the network and **propagates**  the change to the nearby nodes.

1. All the nodes which receives it will validate the proof of work and then add it to their respective copies. If it is not valid, then the block is not added to the chain.

1. When there is a conflict in the network , then the “longest chain rule” is applied to resolve it. Lets say two miners claim the same block and both have valid proof of work. Then the longest chain rule is applied which is whichever miner has the longest chain of blocks will be taken as the winner and that is added to the blockchain.

## Ethereum

![](https://cdn-images-1.medium.com/max/16000/1*AReX8uZOZKpGcvuUjogh0g.png)

Now that you have got a grasp of blockchain lets move ahead with Ethereum. Ethereum is a **decentralized platform that** allows us to write applications that run exactly as programmed without any possibility of downtime, censorship, fraud or third party interference. It consists of Ethereum Virtual Machine(EVM) which provides the container in which all the smart contracts can be executed.

### Smart contracts

Ethereum allows us to write applications on the blockchain and this applications are known as smart contracts. These smart contracts reside on the blockchain and they are **immutable**  in nature, ie. the code cannot be deleted or modified in the blockchain once it is deployed. This can be written using Solidity or other languages, but the most preferred is solidity. It is a turing complete language.

### Ether

Ether is the cryptocurrency used in the Ethereum blockchain.

### Accounts

In Ethereum, the state is made up of objects called “accounts”, with each account having a 20-byte address and state transitions being direct transfers of value and information between accounts. There are two types of accounts in Ethereum:

* **Externally owned accounts :** These accounts are owned by users, controlled by private keys. An externally owned account has no code, and one can send messages from an externally owned account by creating and signing a transaction.

* **Contract accounts:** These accounts are owned by contract code. In a contract account, every time the contract account receives a message its code activates, allowing it to read and write to internal storage and send other messages or create contracts in turn.

### Gas

As smart contracts are turing complete any infinity loop or other code can be written and the blockchain can be crashed. To prevent from such attacks Ethereum uses a concept called gas. Gas is nothing but some transaction cost which is paid to execute the transaction using Ether(basic currency in Ethereum chain). Each instruction requires some gas to be executed and the gas is sent along with any call that needs to modify the blockchain.

### DAPPS

These are distributed apps that can be built using the smart contracts and providing an interface for the users(accounts). Different kinds of applications can be developed which will interact with smart contracts residing in the blockchain.

### Basic Workflow using Ethereum

We can discuss a basic workflow in Ethereum network for better understanding of how all these concepts work together in unison.

1. We can write smart contracts and deploy it to Ethereum network. Once deployed these contracts cannot be changed.

1. Any account or another smart contract in the network can execute these smart contracts functions through transactions.

1. The smart contracts can be called and executed by sending transactions to the contract. These transactions cost **gas** and a certain gas should also be sent along with the transaction.

1. Sometimes we just need to know the state of some contract without modifying the blockchain. These are known as **calls and they do not cost any gas.** 

1. We can build various Dapps by executing the smart contracts using transactions and calls , thus allowing the user to directly interact the smart contract in different ways.

I believe this post provides basic understanding of the blockchain and Ethereum. In my next post I will provide a detailed guide to getting started with building Dapps using Ethereum.

*If you liked this story, feel free to reach out to me at [https://kaizencoder.com/](https://kaizencoder.com/).*