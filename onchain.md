---
order: 70
icon: link
image: ./static/onchain.png
---

# 100% On-Chain

A very important feature of Punk Domains is that it's a 100% on-chain protocol.

But what does that mean?

### On-chain domain name

The information about which address owns (or resolves to) a domain name is written on the blockchain. 

This seems to go without saying for web3 projects, but there are some projects that present themselves as blockchain domain name services, but in fact store the mapping between a domain name and an address on a centralized server.

A typical web3 domain service would usually give you a domain name in a form of an NFT. While NFTs do exist on a blockchain, there's also an important part of NFTs that's often hosted outside of a blockchain (e.g. on a centralized server): the metadata.

### On-chain metadata

The NFT metadata usually include the following data:

- Name
- Image
- Description

There can be other data present (like attributes/rarities), but in the context of domains the above three are the most important.

The metadata can be stored on three different places:

- **On-chain** (on the blockchain where NFT exists, usually in the same smart contract).
- On a **decentralized storage** system such as IPFS and Arweave.
- On a **centralized server**.

Obviously it's best if metadata is stored on-chain, which means it lives there forever and no one can change it. 

The worst storage for metadata is a centralized server, because the owner of that server can change the data or even delete it completely. It can also happen that the server malfunctions and is not available for some time, or that hard drive gets corrupted and there's no backup (the data is lost forever).

Somewhere in the middle is hosting metadata on IPFS or Arweave. In that case it's important that the web3 domain service is paying for the constant availability of the metadata. If it's not, the metadata can be inaccessible for certain periods of time or even disappear from the system completely (if no IPFS node is incentivized to keep that data, why should they?)

Often NFT creators reserve the right to change the IPFS base URL in their NFT contracts, which means they can change the metadata for your NFT and potentially even steal it (the token ID would remain the same, but data such as name, image, attributes etc. would be completely different). In that case an IPFS storage is no better than a centralized server.

That's why keeping all data completely on-chain is extremely important and this is what Punk Domains does.

**How to find out where NFT metadata is stored?**

The easiest way is to go to the NFT contract on Etherscan (or similar block explorer) and find the **Read section**. This section includes all functions that help you read data stored in a smart contract. 

Then find a function called `tokenURI` and enter some random token ID in it (for example: `1`). And then observe what data do you get back.

A) If you get back a URL that starts with `http`, the metadata is hosted on a **centralized server**.

B) If you get back a URL that starts with `ipfs`, then the metadata is stored on **IPFS**. In that case also check whether the contract has a function called `setBaseURI` (or similar) in the **Write section**. This would allow the NFT project creator to change the IPFS URL and change your metadata (like change the NFT name or image).

C) But if you get data that starts with `string: data:application/json;base64` and after that some big chunk of text that looks like "giberish" (`eyJuYW1lIjogIm5mdC...`), it's very likely **on-chain** metadata that is encoded in a format called base64. You can verify that by decoding the "gibberish" part on a website like this one: https://www.base64decode.org/.

### On-chain other data

Domain name services often allow you to add other data to your domain, not just the associated address. Such data can include things like a homepage URL, Twitter handle, email, phone number, profile picture etc. Adding this additional data is completely optional.

Storing other data on-chain may not be that important as it is for storing metadata and domain name, but it's still better than being stored off-chain.

### Users have complete control over their domain names

This is another thing that seems to go without saying, but not all "web3" domain services follow that approach. We're not going to name names, but it's important that you're aware whether you hold complete control over your domain name, or not. 

With Punk Domains, you're in complete control and you can own your domain name forever (no renewals needed and no one can take your domain from you).

### TLD owners have complete control over their TLDs

Top-level domains (TLDs) are also known as domain extensions (for example, .wagmi, .wagmi, .arbi). If a web3 domain name service offers multiple TLDs that can be owned by different entites, it is very important that TLD owners have complete control over their respective TLDs.

At Punk Domains we focus on **Domains for DAOs**, that's why we feel it's very important that TLD owners control their TLDs. As with domain names, once you own a TLD, you can own it forever. Punk Domains cannot take it from you, you have complete control.