# ERC-20-tutorial

A quick ERC-20 tutorial with testing, fuzzing and more.

## Our Approach

This tutorial will help you learn web3 with three principles in mind:

- Learning by doing
- Starting with blockchain first
- Providing the big picture context for additional learning

By focusing on project-based learning, you will have the proper context to understand new technical concepts. For motivation, it's also good to have an end goal in mind and goal posts along the journey.

As you will see, web3 is an emergent technology, like a skills tree in an RPG game. Innovations and standards in one area unlock the door for new tech built upon it. For example, the ERC-20 standard allows for Decentralized Finance (DeFi) to be possible. The concepts introduced here will expand into other applications.

## Concepts and Tech Covered

### Concepts

We will be covering the following concepts:

- Developing an ERC-20 smart contract
- Understanding what are smart contract standards
- Understanding the smart contract development life cycle
- Creating scripts to automate your work
- Testing, fuzzing and security best practices in context of this project

### Tech

We'll be using the following tools:

- Solidity
- Truffle Suite
- OpenZeppelin
- Infura
- React
- JavaScript
- Web3JS

## Prerequsites

To complete this module, it is assumed that you know **at least the basics** of:

- Programming
- JavaScript
- React
- NodeJS
- Command-line terminal

For those new to programming, check out [ConsenSys Academy's Basic Training](https://consensys.net/blog/developers/introducing-basic-training-a-free-consensys-academy-course-for-software-engineering-fundamentals/), a free course to guide new developers. You can also join our [TBD - Truffle Unleashed Discord Channel]() to chat with other current and aspiring devs on your journey.

You can also message [@tesla809](https://twitter.com/Tesla809) on Twitter if you have a programming question.

<!-- However, if you don't know the basics, this tutorial will have sidenotes with links and explanations on this topic. They will be brief enough to let you understand the basics and get you to the next step.

Once the context is established, it is suggested that you dig deeper into those concepts later. -->

If you are curious, check out this [basic introduction to Ethereum](https://ethereum.org/en/developers/docs/intro-to-ethereum/).

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

Basically, a token contract is some code that maps addresses to balances with additional methods to alter those balances.

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

The [ERC-20 standard](https://eips.ethereum.org/EIPS/eip-20) defines a common list of rules that all fungible Ethereum tokens should adhere to. Without adherance, developers will find it hard for others to use their token, reducing its utility and possible network effects.

The purpose of the ERC-20 standard is to make any token implementation interoperable, reusable and composable across any application, like wallets, decentralized exchanges, lending markets and beyond. It provides the basic functionality to transfer tokens and allow tokens to be approved, so they can be spent by another on-chain third party. This common standard creates the building blocks for Decentralized Finance (DeFi).

EatTheBlock's video on [Ethereum Tokens: ERC20 Tutorial (transfer, transferFrom, approve...)](https://www.youtube.com/watch?v=o9Ux3xDrkIo) gives an contextual overview which can be used with this tutorial.

#### The Minumum ERC-20 API

Below are all the required methods and events needed to implement the ERC-20 standard. Again, the ERC-20 standard is just a **common API for fungible assets**.

Let's go through each part of this code and cover:

- SPDX-License-Identifier
- NatSpec
- pragma
- interfaces
- events
- functions

Later, when we implement our first pass at the contract, we will cover the basics of Solidity's language primitives. This may be counter intuitive at first, but starting with the standard allows us to take a big picture hands-on view.

Below is OpenZeppelin's implementation of the minimum required API for the ERC-20 Standard.

```solidity
// SPDX-License-Identifier: MIT
// OpenZeppelin Contracts (last updated v4.6.0) (token/ERC20/IERC20.sol)

pragma solidity ^0.8.0;

/**
 * @dev Interface of the ERC20 standard as defined in the EIP.
 */
interface IERC20 {
    /**
     * @dev Emitted when `value` tokens are moved from one account (`from`) to
     * another (`to`).
     *
     * Note that `value` may be zero.
     */
    event Transfer(address indexed from, address indexed to, uint256 value);

    /**
     * @dev Emitted when the allowance of a `spender` for an `owner` is set by
     * a call to {approve}. `value` is the new allowance.
     */
    event Approval(address indexed owner, address indexed spender, uint256 value);

    /**
     * @dev Returns the amount of tokens in existence.
     */
    function totalSupply() external view returns (uint256);

    /**
     * @dev Returns the amount of tokens owned by `account`.
     */
    function balanceOf(address account) external view returns (uint256);

    /**
     * @dev Moves `amount` tokens from the caller's account to `to`.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * Emits a {Transfer} event.
     */
    function transfer(address to, uint256 amount) external returns (bool);

    /**
     * @dev Returns the remaining number of tokens that `spender` will be
     * allowed to spend on behalf of `owner` through {transferFrom}. This is
     * zero by default.
     *
     * This value changes when {approve} or {transferFrom} are called.
     */
    function allowance(address owner, address spender) external view returns (uint256);

    /**
     * @dev Sets `amount` as the allowance of `spender` over the caller's tokens.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * IMPORTANT: Beware that changing an allowance with this method brings the risk
     * that someone may use both the old and the new allowance by unfortunate
     * transaction ordering. One possible solution to mitigate this race
     * condition is to first reduce the spender's allowance to 0 and set the
     * desired value afterwards:
     * https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729
     *
     * Emits an {Approval} event.
     */
    function approve(address spender, uint256 amount) external returns (bool);

    /**
     * @dev Moves `amount` tokens from `from` to `to` using the
     * allowance mechanism. `amount` is then deducted from the caller's
     * allowance.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * Emits a {Transfer} event.
     */
    function transferFrom(
        address from,
        address to,
        uint256 amount
    ) external returns (bool);
}
```

#### Comments

Programming languages have the abilty to allow developers to leave comments. Solidity follows the JavaScript (ECMAScript) style of making comments with:

- `//` single line comments
- `/* */` multi line comments

#### SPDX

Solidity files should have a license identifier. Software licenses are essential because, depending on the type, they can provide different limitations, liability protection, or requirements for usage. Usually, smart contracts use the [MIT License](https://choosealicense.com/licenses/mit/), which limits personal liability while giving users expansive freedoms.

If you need a different license, explain it in the comments. In addition, you can find a [developer's guide to licenses here](https://github.com/readme/guides/open-source-licensing) and, for the more curious, the entire [list of SPDX licenses here](https://spdx.org/licenses/). Reasons for choosing a different license range from business considerations to wishing to retain all derivative code as open-source even if a business builds on top of it.

[SPDX](https://spdx.dev/) is an open standard for communicating software licenses, copywrites, security references, etc.

#### OpenZeppelin Reference

[OpenZeppelin](https://www.openzeppelin.com/) provides security products to build, automate, and operate decentralized applications. OpenZeppelin's Solidity smart contracts are a library of modular, reusable, secure smart contracts for EVM-based networks. Used by the Ethereum Foundation and the world's top protocols, they are the industry standard and provide a secure base for developing your smart contracts.

Later, we'll see how we import their contracts to provide a secure base for our smart contracts.

#### NatSpec

The multiline comments with symbols like `@dev` are part of Solidity's [NatSpec](https://docs.soliditylang.org/en/develop/natspec-format.html) format. NatSpec is used to produce documentation from the source code. JavaScript Developers may recognize its similarity to [JSDoc](https://jsdoc.app/about-getting-started.html). Using NatSpec to document your code is [considered a security best practice](https://ethereum.org/en/developers/tutorials/smart-contract-security-guidelines/#documentation-and-specifications).

NatSpec is useful for developers, 3rd party tooling, and end-users. For developers, it helps them and the future you understand your code. Custom annotations used by 3rd party tools can be added. NatSpec messages may even be shown to the end-user at the time that they will interact with the contract, like signing a transaction.

There are other symbols like:

- @title - A title that should describe the contract/interface

- @author - The name of the author

- @notice - Explain to an end user what this does

- @dev - Explain to a developer any extra details

- @param - Documents a parameter just like in Doxygen (must be followed by parameter name)

- @return - Documents the return variables of a contract’s function

- @custom: - Custom tag, semantics is application-defined

#### Pragma

`pragma solidity >=0.6.0 <0.8.0;`

Since what is executed on the Ethereum Virtual Machine (EVM) is EVM bytecode, any language that compiles into it can be used to write smart contracts. Another popular language is [Vyper](https://vyper.readthedocs.io/en/stable/), a Python-inspired smart contract scripting language for the EVM. Check this [quick breakdown of both](https://ethereum.org/en/developers/docs/smart-contracts/languages/) if you are curious. Hence, because of various languages, in our pragma, we specify the language.

Like all programming languages, Solidity has updates. The `pragma` states which version of the Solidity is being used. The pragma determines which compiler to use to [compile the code to EVM Bytecode](https://ethereum.org/en/developers/docs/smart-contracts/compiling/). This is important because Solidity becomes safer and easier to use as the language evolves. The version of the language is indicated by the [Semantic versioning](https://www.geeksforgeeks.org/introduction-semantic-versioning/) (SemVer). Depending on what symbol you pass in, you can indicate which compiler version to use. See this [simple SemVer cheat sheet](https://devhints.io/semver).

`>=0.6.0 <0.8.0;` indicates to use the compiler greater than 0.6.0 and less than 0.8.0. Specifying the minimum and maximum range of a language with which you tested the code is a good practice.

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

#### Events

As mentioned before, [Events](https://www.thirdandgrove.com/insights/ethereum-part-iv-contract-events-and-logs/#:~:text=An%20event%20allows%20a%20contract,data%20about%20the%20state%20change.) are used to issue alerts regarding actions that occurred on the blockchain. Apps can subscribe to events to update their UI. Events can also be used for logging purposes. Event "emits" a message when an action on a function occurs.

A deeper dive into [Events can be found in this video](<[Events](https://www.youtube.com/watch?v=nopo9KwwRg4)>).

Note three things:

- Event start with a captial lettter
- Event don't modify the smart contract's state related to account. However, they DO modify the blockchain as described Solidity Language [forum](https://ethereum.stackexchange.com/questions/127152/events-can-cause-state-change) and [in this StackOverflow post](https://ethereum.stackexchange.com/questions/127152/events-can-cause-state-change).
- A good and practical description of Events can be found in the introduction of [Understanding event logs on the Ethereum blockchain by Luit Hollander](https://medium.com/mycrypto/understanding-event-logs-on-the-ethereum-blockchain-f4ae7ba50378).

An additional note on syntax. Don't get hung up on understanding each part immediately. We will get into the specifics later during our implementation. For now, just understand the big picture and gist of the code.

##### Transfer

```solidity
/**
 * @dev Emitted when `value` tokens are moved from one account (`from`) to
 * another (`to`).
 *
 * Note that `value` may be zero.
 */

event Transfer(address indexed from, address indexed to, uint256 value);
```

The `Transfer` event is emitted when the amount of tokens, `value`, is sent from the `from` address to the `to` address.

##### Approval

```solidity
/**
 * @dev Emitted when the allowance of a `spender` for an `owner` is set by
 * a call to {approve}. `value` is the new allowance.
 */

event Approval(address indexed owner, address indexed spender, uint256 value);
```

This event is emitted when the amount of tokens (value) is approved by the owner to be used by the spender.

#### Getter Functions

Getters are functions that only read and return data from the smart contract on the Ethereum network. They DO NOT modify the state of the contract, i.e. updating or deleting information.

##### totalSupply

```solidity
/**
 * @dev Returns the amount of tokens in existence.
 */

function totalSupply() external view returns (uint256);
```

`totalSupply()` **returns the amount of tokens in existence**.

This function is:

- a getter
- does not modify the state of the contract.
- Interestingly, Solidity does not have `floats`. `float` or floating-point numbers represent decimal numbers in other languages. This is similar to how `int` represents integers or `string` represents words. These are considered language 'primitives', building blocks of the language.

So, how do we represent a fraction of a unit of value? An example is 0.5 US dollars (50 cents) or 0.5 ETH?

Let's describe briefly, then go in-depth later during our custom ERC-20 contract implementation.

We see local currencies adopt two decimal subdivisions in everyday life, i.e., $USD 1.50. In Ethereum, most tokens are even more subdivisible, and most adopt 18 decimals. As a result, most will return the `totalSupply` as `1000000000000000000` for `1 token`. However, this is not universal, and you should check when dealing with 3rd party tokens.

##### balanceOf

```solidity
/**
 * @dev Returns the amount of tokens owned by `account`.
 */

function balanceOf(address account) external view returns (uint256);
```

`balanceOf()` **returns the amount of tokens owned by an address (account).**

This function:

- is a getter
- does not modify the state of the contract.

What is an [`address`](https://docs.soliditylang.org/en/v0.8.14/types.html?highlight=address#address)? `address` represents [accounts](https://ethereum.org/en/developers/docs/accounts/) in Solidity, which you can think of as bank accounts. For the computer science-oriented, `address` can be regarded as memory locations in a computer.

Accounts are what "hold" your digital assets. As we read before, contracts have a "ledger" via a key-value pair data structure called a `mapping`. The contract holds a record of which `address` holds how much of an asset. When the [wallet](https://ethereum.org/en/wallets/) reads the token contract, it appears as if the token is in the wallet.

##### allowance

```solidity
/**
 * @dev Returns the remaining number of tokens that `spender` will be
 * allowed to spend on behalf of `owner` through {transferFrom}. This is
 * zero by default.
 *
 * This value changes when {approve} or {transferFrom} are called.
 */
function allowance(address owner, address spender) external view returns (uint256);
```

This function:

- is a getter
- does not modify the state of the contract
- **should return 0 by default.**

`allowance()` returns the amount which `spender` is still allowed to withdraw from `owner`. By default, this is zero.

This value changes when `approve()` or `transferFrom()` are called. We will expand on the security implications of `approve()` below and during our custom ERC-20 implementation.

#### Functions

The following functions update the state of the contract. This means they can change data inside the contract, so extra care needs to be added here.

Note that OpenZeppelin Contracts functions will `revert` instead of returning false on failure. `revert` means the contract will undo all state changes, return a value, and refund any remaining gas to the caller.

##### transfer

```solidity
/**
 * @dev Moves `amount` tokens from the caller's account to `to`.
 *
 * Returns a boolean value indicating whether the operation succeeded.
 *
 * Emits a {Transfer} event.
 */
function transfer(address to, uint256 amount) external returns (bool);
```

This function:

- Modifies the state of the contract
- `reverts` if failure occurs
- returns `true` if transfer is possible

`transfer()` moves an `amount` of tokens from the function caller’s `address` to recipient's `address`. Then it emits the Transfer event defined later. It returns true if the transfer was possible.

##### approve

```solidity
/**
 * @dev Sets `amount` as the allowance of `spender` over the caller's tokens.
 *
 * Returns a boolean value indicating whether the operation succeeded.
 *
 * IMPORTANT: Beware that changing an allowance with this method brings the risk
 * that someone may use both the old and the new allowance by unfortunate
 * transaction ordering. One possible solution to mitigate this race
 * condition is to first reduce the spender's allowance to 0 and set the
 * desired value afterwards:
 * https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729
 *
 * Emits an {Approval} event.
 */
function approve(address spender, uint256 amount) external returns (bool);
```

This function:

- Modifies the state of the contract
- Returns a boolean (true/false) value if sent
- `reverts` if failure occurs

`approve()` sets the amount of allowance the spender is allowed to transfer from the function caller (msg.sender) balance. This function emits the `Approval` event. Finally, `approve()` returns whether the allowance was successfully sent.

Why is this useful? Allowing another address to use your tokens opens the door for payments, escrow, and all sorts of financial transactions without having to approve. Through `approve()`, you give another on-chain entity the ability to use funds as they see fit.

##### Unlimited permissions on approve() as a security flaw

However, your Spidey senses may be tingling now.

Basically, "Infinite approval means Infinite trust, something you shouldn't have in DeFi or any legal contract."

Infinite approvals are akin to giving complete control over your account's assets to a third party. Convenient to get stuff done until things go wrong.

[Here is a video by Paul Razvan Berg at DevCon V briefly describing the problem](https://youtu.be/y9A8wHhNjJA)

The improper use of `approve()` opens the door for hacks and scammers. **In fact, this is a common way for hackers to trick users into stealing their funds.**

How does this happen? Say a user wants to deposit 100 SAMPLEToken, an ERC-20 token, into another contract. The user can set `approve()` as the EXACT amount. However, what if the user plans to deposit funds again later? This would mean approving and spending funds to do so several times. Due to this friction, many apps instead request an unlimited allowance from the user. With unlimited allowance, the user only needs to approve once and on every future deposit.

The root motivation of "unlimited approval" are:

- less friction, since two transactions are required for both `approve()` and `transferFrom()`.
- for cheaper fees, since the cost of interacting with the contract can rise based on network demand due to [gas fees](https://ethereum.org/en/developers/docs/gas/).
- better UX, since asking approval occurs only once, thus being unlimited.

Here is the gotcha moment. **By giving contracts unlimited permissions on `approve()`, you expose the risk of having all your tokens stolen.** This includes:

- the deposited funds
- AND the tokens held "safely" in your wallet.

Note that you are still vulnerable to these types of smart contract exploits even if your:

- your secret recovery phrase (seed phrase) is not shared
- private keys are secured in a hardware wallet

This exploit can occur even in legitimate protocols that do not intend to scam their users. Hackers can leverage unlimited permissions and combine them with exploits to drain the funds of legitimate projects, like what happened with [Bancor](https://medium.com/zengo/bancor-smart-contracts-vulnerability-and-its-lessons-ce762d09bb9a), [Furucombo via Rekt.news](https://rekt.news/furucombo-rekt/), [DeFi Saver](https://medium.com/defi-saver/disclosing-a-recently-discovered-exchange-vulnerability-fcd0b61edffe), [BadgerDAO](https://rekt.news/badger-rekt/) and other projects.

Another way to scam users is by [airdropping scam tokens in their wallet](https://medium.com/mycrypto/bad-actors-abusing-erc20-approval-to-steal-your-tokens-c0407b7f7c7c). To accept the tokens users give unlimited permissions to the token. Then, the tokens that specific account are stolen.

It is HIGHLY suggested to read the article ["Unlimited ERC20 allowances considered harmful" by Rosco Kalis](https://kalis.me/unlimited-erc20-allowances/) on the topic. The author outlines an excellent description of the problem, case studies of hacks, and possible solutions. Another great article with a great step-by-step visual breakdown of the issues can be found by [Blocksecteam](https://blocksecteam.medium.com/unlimited-approval-in-erc20-convenience-or-security-1c8dce421ed7). An [high-level description of unlimited permissions](https://coinmarketcap.com/alexandria/glossary/infinite-approval) can be found via Coinmarketcap.

You can learn [how to revoke unlimited permissions via this article by Bankless](https://newsletter.banklesshq.com/p/how-to-protect-your-ethereum-wallet). Additionally, you can check and revoke token approvals via [EtherScan.io](https://etherscan.io/tokenapprovalchecker).

There are things we can do to mitigate this. First, there are safer ways to implement `approve()`. We will go in-depth into this during our Custom ERC-20 token implementation and discuss [EIP-712](https://eips.ethereum.org/EIPS/eip-712) and [EIP-2612](https://eips.ethereum.org/EIPS/eip-2612). Additionally, we can do things on the front end to alert the user, which we will cover in our front section.

For now, let's continue with understanding ERC-20s.

##### transferFrom

```solidity
/**
 * @dev Moves `amount` tokens from `from` to `to` using the
 * allowance mechanism. `amount` is then deducted from the caller's
 * allowance.
 *
 * Returns a boolean value indicating whether the operation succeeded.
 *
 * Emits a {Transfer} event.
 */
function transferFrom(
    address from,
    address to,
    uint256 amount
) external returns (bool);
```

This function:

- Modifies the state of the contract
- Returns a boolean (true/false) value if sent
- `reverts` if failure occurs

`transferFrom()` moves the amount of tokens from sender to recipient using the `allowance` mechanism. Then `amount` deducted from the caller’s allowance. This function emits the Transfer event.

##### Multiple transferFrom() calls as a security flaw

OpenZeppelin's [ERC-20 documentation](https://docs.openzeppelin.com/contracts/2.x/api/token/erc20#IERC20-approve-address-uint256-) mentions the risk of someone using both the old and the new allowance by [unfortunate transaction ordering](https://ethereum-contract-security-techniques-and-tips.readthedocs.io/en/latest/known_attacks/#transaction-ordering-dependence-tod-front-running).

- N: old transaction approving N tokens
- M: new transaction approving M tokens
- N + M: transaction approving N + M tokens.

We will discuss how to deal with this issue during our implementation. For the curious, a great breakdown can be found in the write up by ["ERC20 API: An Attack Vector on the Approve/TransferFrom Methods" by Mikhail Vladimirov and Dmitry Khovratovich](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit#).

#### Optional ERC-20 Methods

If you notice the [ERC-20 standard](https://eips.ethereum.org/EIPS/eip-20#methods) has optional methods.

Let's cover these and provide some context.

Please note that these following OPTIONAL Getter methods can be used to improve usability, BUT interfaces and other contracts MUST NOT expect these values to be present.

These optional methods can be found in OpenZeppelin's [ERC20Detailed](https://docs.openzeppelin.com/contracts/2.x/api/token/erc20#ERC20Detailed) contract.

Later, we will discuss how to extend our ERC-20 implementation to include this optional contract using multiple inheritance.

##### name

`function name() public view returns (string)`

This function:

- is a optional getter method
- Returns the name of the token - e.g. "MyToken".

`symbol()` returns the token ticker, which is used by wallets and other applications to display the token.

##### symbol

`function symbol() public view returns (string)`

This function:

- is a optional getter method
- Returns the symbol of the token. E.g. “HIX”.

`name()` returns the token ticker, which is used by wallets and other applications to display the token.

##### decimals

`function decimals() public view returns (uint8)`

This function:

- is an optional getter method
- Returns the granularity the token can be divided into via the number of decimals the token uses.

Returns the token's granularity, i.e., how small it can be divided into, via the number of decimals the token uses.

Recall that Solidity does not have `float` for decimals. So how could we deal with fractional portions of tokens like 0.5 SAMPLEToken?

There is a simple solution: All math is done by using large numbers which represent smaller numbers. Most tokens use the same granularity as Ether, with the smallest denomination being 10\*\*-18 or 18 places after the decimal (0.000000000000000001). In Ethereum, the smallest denomination is called a wei.

Note: In Solidity, the operator for exponents is \*\*.

The breakdown of the logical:
1 wei = 0.000000000000000001 ETH
10 wei = 0.000000000000000010 ETH
100 wei = 0.00000000000000100 ETH
1000 wei = 0.00000000000001000 ETH
...
1000000000000000000 wei = 1.000000000000000000 = 1 ETH

If we follow the same logic:
1 = 0.000000000000000001 SAMPLEToken
10 = 0.000000000000000010 SAMPLEToken
100 = 0.00000000000000100 SAMPLEToken
1000 = 0.00000000000001000 SAMPLEToken
...
1000000000000000000 = 1.000000000000000000 = 1 SAMPLEToken

Logically, to represent 0.5 SAMPLEToken our number will be:
0.5 SAMPLEToken = 500000000000000000

OpenZeppelin's [ERC-20 implementation](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#ERC20-decimals--) makes this easy by providing a `decimal` variable to hold our decimal's granularity. This is used to help with the code's presentation to applications like wallets for end users to understand. The variable DOES NOT affect the integer arithmetic.

We will cover this deeper in our implementation.

EatTheBlocks' [ERC-20 video](https://youtu.be/o9Ux3xDrkIo?t=205) describes `decimals()` in depth. Additionally, OpenZeppelin's [ERC-20 overview](https://docs.openzeppelin.com/contracts/4.x/erc20#a-note-on-decimals) explains how this works. We will go indepth on how to apply this during our implementation phase.

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

### approve() side quest

Here is a [side quest](https://medium.com/@rodrigoherrerai/understanding-the-problem-of-erc20-unlimited-approval-from-first-principles-d2eaf6b4ea0e) to understand why unlimited permissions from approve are dangerous.

## ERC-20 Extensions

### Minting and Burning Overview

When minting new tokens, the transfer is usually from the 0x00..0000 address. When burning tokens the transfer is **to** 0x00..0000.

#### ERC20Mintable

#### ERC20Capped

#### ERC20Burnable

#### ERC20Pausable

## ERC-20 Safety

### Time Locks

### SafeERC20
