# ERC-20-tutorial

A quick ERC-20 tutorial with testing, fuzzing and more.

## Background Overview

### What is a Token

First, let's understand what a token is. Conceptually, a token is a representation of some asset in the blockchain. Since blockchains are great for modeling economic scarcity by determining who owns what, this asset would most likely be scarce and owned by some entity.

Tokens can represent anything, like time, money, services, virtual pets, stock, bonds, video game points, characters, items, reputation points, ounces of gold, and much more.

### Token Contracts

Under the hood, a token is just a smart contract. In fact, most things built on Ethereum are smart contracts, which are programmable snippets of code that run on the Ethereum blockchain.

#### Token Methods

Token contracts define the actions which a token can perform. Actions like "sending tokens" and "destroying tokens" are just really programmed functions in the contract.

#### Token State

Token contracts also hold "state," which is data associated with the token, like the balance of all token holders. Within the contract, there is a key-value data structure called a "mapping," which holds the balances of each address. This "ledger" is what determines who owns what.

#### Example: Moving Tokens

When a token moves from one address to another, the token doesn't move from one wallet to another. Instead, it's similar to a database update or a spreadsheet, where one account's funds are reduced, and another is increased.

#### Custom logic

Since token contracts are programs, you can create any sort of logic based on this move. In theory, you can create a token that gives 2x the amount you sent to the recipient. You are only limited by your imagination.

### What is an ERC-20 Token

#### Fungible Goods

An ERC20 token is used to represent fungible goods. [Fungible goods](https://en.wikipedia.org/wiki/Fungibility) are equivalent and interchangeable. Therefore, each token is exactly the same, with no token having any special behavior attached to it.

Examples of fungible goods are Ether, fiat currencies like the US Dollar or Euro, and voting rights. ERC-20 tokens are useful for assets like currencies, voting rights, points in a game, and more. In general, with fungible assets, you care about how much of it you have.

### ERC-20 Standard

#### What are token standards

Simply put, a token standard is **a common API** for tokens within smart contracts.

Token standards allow developers to predict how to interact with other tokens. Since smart contracts can be programmed in any way, **standards** need to be created so that tokens interoperate with each other and other contracts. Without standards, there would be as many implementations as there are tokens. Building any composable application that leverages other smart contracts would be difficult and time-consuming.

Token standards have a minimum required common set of methods and events. Their naming must be the same as the standard. However, their implementation or underlying logic is open to the developer. Once this minimum set of methods and events have been satisfied, the token can have additional methods and interfaces for added functionality.

Events are used to issue alerts regarding actions that occured on the blockchain. Events can be used to trigger UI updates on app front ends, testing, logging and more.

### ERC-20 Standard Overview

The ERC-20 standard defines a common list of rules that all fungible Ethereum tokens should adhere to. Without adherance, developers will find it hard for others to use their token, reducing its utility and possible network effects.

#### ERC-20 API

```solidity
pragma solidity ^0.6.0;

interface IERC20 {

    function totalSupply() external view returns (uint256);
    function balanceOf(address account) external view returns (uint256);
    function allowance(address owner, address spender) external view returns (uint256);

    function transfer(address recipient, uint256 amount) external returns (bool);
    function approve(address spender, uint256 amount) external returns (bool);
    function transferFrom(address sender, address recipient, uint256 amount) external returns (bool);


    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);

}
```

#### Getters

#### Setters

#### Functions

#### Events

## Setup

### Via Github

You can fork and clone this repo

Fork repo then run

```console
git clone YOUR-GITHUB-URL
```

### Manual Setup

Or you can set up the repo from scratch. Knowing how to do this is helpful if you are creating an independent project in the future.

Create the repository

```console
mkdir erc-20-tutorial
```

Set up Truffle Suite. Truffle is a suite of tools and a community to help you get to professional-grade development.

```console
truffle init
```

Setup package.json. Use the `-y` flag to skip over setup config questions.

This will automatically answer yes to all questions which may have security implications. For our purposes, this will not matter.

```console
yarn init -y
```

Set up the front end

```console
npx create-react-app client
```

## Basic ERC-20
