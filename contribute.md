---
order: 30
icon: question
images: "https://blog.punk.domains/img/contribute/cover.jpg"
---

# How to contribute to Punk Domains

As you already know, Punk Domains is a web3 domains protocol that can issue domain extensions for DAOs and other web3 communities.

Some of the protocol clients include renowned names such as KlimaDAO (.klima domain extension), Layer2DAO (.L2), Smol Brains NFT community (.smol), PoolTogether (.pool), etc.

As it's common with open-source software, Punk Domains protocol is **developed and maintained by contributors**.

## What is a contributor

A contributor is a volunteer that uses their time and skills to benefit the project. Being a contributor is usually not a paid position, although contributors may get rewards for their past work.
  
![Photo by Irvan Smith on Unsplash](https://blog.punk.domains/img/contribute/coder.jpg)

## How people contribute to projects

Contributions can come in many shapes and forms, from non-technical contributions such as community management, content writing and facilitating new partnerships, to more technical ones such as software development.

When it comes to technical contributions within the Punk Domains project, we can split it further in two categories:

- Core protocol development
- Development for clients

## Core protocol development

The core protocol development mainly involves working on Punk Domains smart contracts written in Solidity. A contributor can, for example, build a new TLD Factory that has a different set of features than the existing factories.

Core protocol development is in most projects the most challenging way of contributing, because it requires deep understanding of how the protocol works.

But if you are new to the project, do not be afraid, there are other, easier ways to contribute, such as development for clients. This way you can learn more about the protocol by starting with smaller/easier tasks, and progress to more challenging ones later on.

## Development for clients

When some DAO or a web3 community reaches out to us to issue them their own unique domain extension, we usually also help them set up a Minter smart contract and a dedicated frontend for minting and managing domains.

### Minter contract development for clients

A Minter is a smart contract with a custom set of rules that define who is allowed to mint new domains, different pricing models, etc.

For example, an NFT community can decide to have a Minter contract that provides a special discount on domain minting to anyone who holds their NFT.

A contributor can set up such a smart contract for the client, and can also be rewarded for the work by the client. The reward can either be a one-time payment, an NFT, a share of each domain minting payment (this can be coded into the Minter contract), or something else that they agree on.

There are a bunch of already developed Minter smart contracts [in our GitHub repository](https://github.com/punk-domains/punk-contracts/tree/main/contracts/partners), so it's just a matter of finding the one that fits the client's use case the most and tweaking it a bit if needed.

### Front-end development for clients

Most clients wish to have their own frontend for minting domain names, with their own branding and colors.

![Frontend for People Domains](https://blog.punk.domains/img/ppl-joie/ppl-domains.png)

It does not make sense to reinvent a wheel each time, that's why we have a [frontend template](https://github.com/punk-domains/punk-fe-template) (written in Vue.js) that we use for any new client. 

What a contributor needs to do is just clone this template and tweak it based on the client's needs (changing colors, brand name, adding the correct smart contract addresses etc.)

Because there are already plenty of templates for both Minting contracts and for frontends, all the development needed for clients can only take a couple of days.

## Reach out if you'd like to contribute

If you'd like to become a Punk Domains contributor, feel free to reach out via [Discord](https://discord.gg/8dSrwrAQeu) and someone from the existing contributors team will help you onboard. 

Currently people experienced with **Vue** can contribute the most in terms of technical contributions.

We're looking forward to meet you!

> *Note that being a Punk Domains contributor is **not a paid position**, but we still try to find ways to reward meaningful past work. The most straightforward way of being rewarded for your work is by doing development for clients, where you can get a share of each domain minting payment (automated in the Minter contract).*
