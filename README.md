# ERC-20-tutorial

A quick ERC-20 tutorial with testing, fuzzing and more.

## Prerequsites

To complete this module, it is assumed that you know **at least the basics** of:

- Programming
- JavaScript
- React
- NodeJS
- Command-line terminal

For those new to programming, check out [ConsenSys Academy's Basic Training](https://consensys.net/blog/developers/introducing-basic-training-a-free-consensys-academy-course-for-software-engineering-fundamentals/), a free course to guide new developers. You can also join our [TBD - Truffle Unleashed Discord Channel]() to chat with other current and aspiring devs on your journey.

You can also message [@tesla809](https://twitter.com/Tesla809) on Twitter if you have a programming question.

### Note on Solidity

Solidity is a programming scripting language to create smart contracts on Ethereum Virtual Machine (EVM) based blockchains. Ethereum was the first programmable blockchain that allows any arbitrary logic. Bitcoin has scripting capabilities, but it is severely limited.

Familiarity with Solidity is not required but is nice to have. Along the way, we will describe the basics to complete the module. Via hands-on experience, you will be able to pick up the language. If you are stuck, there are resources online to help, like the [official Solidity documentation](https://docs.soliditylang.org/en/v0.8.14/) and [solidity-by-example.org](https://solidity-by-example.org/).

Later, we plan to create stand-alone bite-sized Solidity examples, similar to [Rust by Example](https://doc.rust-lang.org/rust-by-example/index.html).

If you would like a [basic overview of the Ethereum Stack checkout this article](https://ethereum.org/en/developers/docs/ethereum-stack/). Additionally, you can [explore the architecture of a web3 application](https://www.preethikasireddy.com/post/the-architecture-of-a-web-3-0-application).

## Background Overview

### What is a Token

First, let's understand what a token is. Conceptually, a token is a representation of some asset in the blockchain. Since blockchains are great for modeling economic scarcity by determining who owns what, this asset would most likely be scarce and owned by some entity.

Tokens can represent anything, like time, money, services, virtual pets, stock, bonds, video game points, characters, items, reputation points, ounces of gold, and much more.

### Token Contracts

Under the hood, a token is just a smart contract. In fact, most things built on Ethereum are smart contracts, which are programmable snippets of code that run on the Ethereum blockchain.

#### Contracts

[Contracts](https://docs.soliditylang.org/en/v0.8.13/contracts.html) work just like classes in other programming languages. According to the [official Solidity documentation](https://docs.soliditylang.org/en/v0.8.13/introduction-to-smart-contracts.html), a contract is "a collection of code (its functions) and data (its state) that resides at a specific address on the Ethereum blockchain."

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

The purpose of the ERC-20 standard is to make any token implementation interoperable, reusable and composible across any application, like wallets, decentralized exchanges, lending markets and beyond. This common standard creates the building blocks for Decentralized Finance (DeFi).

#### The ERC-20 API

Below are all the required methods and events needed to implement the ERC-20 standard. Again, the ERC-20 standard is just a **common API for fungible assets**.

Let's go through each part of this code and cover:

- pragma
- interfaces
- functions
- events

Later, when we implement our first pass at the contract, we will cover the basics of Solidity's language primitives.

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

#### Pragma

`pragma solidity ^0.6.0;`

Since what is executed on the Ethereum Virtual Machine (EVM) is EVM bytecode, any language that compiles into it can be used to write smart contracts. Another popular language is [Vyper](https://vyper.readthedocs.io/en/stable/), a Python-inspired smart contract scripting language for the EVM. Check this [quick breakdown of both](https://ethereum.org/en/developers/docs/smart-contracts/languages/) if you are curious. Hence, because of various languages, in our pragma, we specify the language.

Like all programming languages, Solidity has updates. The `pragma` states which version of the Solidity is being used. The pragma determines which compiler to use to [compile the code to EVM Bytecode](https://ethereum.org/en/developers/docs/smart-contracts/compiling/). This is important because Solidity becomes safer and easier to use as the language evolves. The version of the language is indicated by the [Semantic versioning](https://www.geeksforgeeks.org/introduction-semantic-versioning/) (SemVer) `^0.6.0;`. The `^` means "compatible with." Depending on what symbol you pass in, you can indicate which compiler version to use. See this [simple SemVer cheat sheet](https://devhints.io/semver).

#### Interface Overview

Think of interfaces like a light switch. Light switches can come in different styles and operate in different ways. However, your only concern is that the lights can be turned on or off. You can think of the light switch as an interface or API for an action, toggling between lights on or off.

In Object-Oriented Programming, [interfaces](<https://en.wikipedia.org/wiki/Interface_(computing)#In_object-oriented_languages>) are popular patterns as well. They split a piece of code's expected functionality from its implementation. Or simply put, interfaces separate the definition of a function from the actual behavior of the said function. As a result, they can help create the APIs that form our token standards.

In Solidity specifically, an Interface is a smart contract that lists a series of functions and events without implementation. Interface contracts do not focus on HOW a contract can do something, only WHAT they can do. Think of smart contract interfaces as a skeleton or backbone. It defines the contract's functionalities and how to trigger them. But not HOW it occurs. HOW the function is implemented is customizable and up to the developer.

The main idea behind interfaces is to provide a re-usable and customizable approach for creating smart contracts. Interface contracts give the structure to create a token standard that serves as the API surface for your contracts.

Just like an API, a smart contract based on a specific interface makes it easy to understand:

- the contract's functionality
- how to interact with the contract.

This allows developers and other contracts a predictable way to interact with any smart contract implementing a specific interface.

By convension, Interface contracts are in named in the form `ITokenStandard`, with `I` and appended by the standard. The ERC-20 standard is thus: `interface IERC20 {...}`. Convention means that it's the HIGHLY suggested manner to do something. However, it is not enforced by the language's compiler.

How are interfaces implemented? Like other programming languages, the implementation class (contract) will inherit from the interface class (contract). However, stay tuned.

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

For context, here is an [overview of an anatomy of a smart sontract](https://ethereum.org/en/developers/docs/smart-contracts/anatomy/).
