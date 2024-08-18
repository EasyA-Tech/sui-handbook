# The Sui Handbook

Welcome. This is EasyA's legendary handbook. If you want to learn Sui like a legend, then you're in the right place.

# Purpose

This handbook serves as a guide to the Sui ecosystem, geared towards those just joining for the first time. It isn't just a beginners' handbook; it's a legendary handbook. Even if you've already immersed yourself in the ecosystem, you'll find tons of helpful tidbits around here!

# The EasyA App

Of course, the best place to start is always the [EasyA](https://www.easya.io) app! Download it here for the fastest and most fun way to learn about Sui. Download it directly right [here](https://links.easya.io/links/gotoapp)!

## Table of Contents

- [Introduction](#introduction)
- [Getting Started](#getting-started)
- [Core Concepts](#core-concepts)
- [Development Tools](#development-tools)
- [Smart Contracts](#smart-contracts)
- [Sui Network](#sui-network)
- [Ecosystem Projects](#ecosystem-projects)
- [Resources](#resources)
- [Handy Code Snippets](#handy-code-snippets)
- [Contributing](#contributing)

## Introduction

What is Sui:

- [Sui Website](https://sui.io) - The official website providing an overview of Sui.

## Getting Started

The no-fluff starter:

- [Installation](https://docs.sui.io/build/install) - Official guide to install Sui and start developing.
- [Learn](https://docs.sui.io/learn) - Comprehensive learning resources for understanding Sui's architecture and concepts.
- [Sui Move by Example](https://examples.sui.io/) - A practical guide to learning Sui Move through examples.

## Core Concepts

Explanation of fundamental concepts in the Sui ecosystem:

- [Programming with Objects](https://docs.sui.io/build/programming-with-objects) - Learn about Sui's object-centric model for smart contract development.
- [Move Patterns](https://www.move-patterns.com/) - A book on Move software design patterns, applicable to Sui development.

## Development Tools

Key tools and environments for Sui:

- [Sui CLI](https://docs.sui.io/build/cli-client) - Command-line interface for interacting with the Sui network.
- [Sui Explorer](https://suiexplorer.com/) - Official block explorer for the Sui network.
- [Move Analyzer VSCode Extension](https://github.com/movebit/sui-move-analyzer) - Enhances the development experience for Move and Sui Move in Visual Studio Code.

## Smart Contracts

How to write and deploy smart contracts on Sui:

- [Sui Smart Contracts](https://docs.sui.io/build/move) - Guide to writing and deploying smart contracts using Sui Move.
- [Move Book](https://move-book.com/) - Comprehensive guide to the Move programming language.

## Sui Network

Going into the network level:

- [Sui Mainnet RPC](https://docs.sui.io/build/json-rpc) - Information on connecting to Sui network.
- [Sui Testnet](https://docs.sui.io/build/testnet) - Details on Sui's testnet for development and testing.

## Ecosystem Projects

Cool projects built on Sui:

- [Sui Wallet](https://github.com/MystenLabs/sui/tree/main/apps/wallet) - Official wallet for managing assets on the Sui network.
- [Cetus](https://app.cetus.zone/) - Decentralized exchange built on Sui.
- [Scallop](https://scallop.io) - Lending protocol on Sui.

...and of course many more - check them out in the EasyA app!

## Resources

Extra stuff:

- [Sui Blog](https://sui.io/blog) - Official blog with updates and insights into Sui development.
- [Sui GitHub](https://github.com/MystenLabs/sui) - The main repository for Sui's development.

## Handy Code Snippets

Get a taste of Sui development with these code snippets:

### Creating a simple coin

```move
module examples::mycoin {
    use sui::coin;

    /// The type identifier of coin. The coin will have a type
    /// tag of kind: `Coin<package_object::mycoin::MYCOIN>`
    /// Make sure that the name of the type matches the module's name.
    public struct MYCOIN has drop {}

    /// Module initializer is called once on module publish. A treasury
    /// cap is sent to the publisher, who then controls minting and burning
    fun init(witness: MYCOIN, ctx: &mut TxContext) {
        let (treasury, metadata) = coin::create_currency(
            witness,
            6,                // decimals
            b"MYC",           // symbol
            b"My Coin",       // name
            b"Don't ask why", // description
            option::none(),   // icon url
            ctx
        );

        // transfer the `TreasuryCap` to the sender, so they can mint and burn
        transfer::public_transfer(treasury, ctx.sender());

        // metadata is typically frozen after creation
        transfer::public_freeze_object(metadata);
    }
}
```

### Init function

```move
module examples::init_function {
    /// The one of a kind - created in the module initializer.
    public struct CreatorCap has key {
        id: UID
    }

    /// This function is only called once on module publish.
    /// Use it to make sure something has happened only once, like
    /// here - only module author will own a version of a
    /// `CreatorCap` struct.
    fun init(ctx: &mut TxContext) {
        transfer::transfer(CreatorCap {
            id: object::new(ctx),
        }, ctx.sender())
    }
}
```

These examples showcase:
1. How to create a simple coin on Sui.
2. How to write an init function.

## Contributing

We welcome contributions to make this handbook even more legendary! Here's how you can contribute:

1. Fork the repository
2. Create a new branch (`git checkout -b feature/amazing-addition`)
3. Make your changes
4. Commit your changes (`git commit -am 'Add some amazing feature'`)
5. Push to the branch (`git push origin feature/amazing-addition`)
6. Create a new Pull Request

Please ensure your contributions align with our code of conduct and contribution guidelines.

## Credit/Inspiration

This handbook was inspired by the famous awesome lists by sindresorhus and the Awesome Sui list. We need awesome lists for Web3 ecosystems, with more of a hacker's guide to how they work. This is the answer to that need.
