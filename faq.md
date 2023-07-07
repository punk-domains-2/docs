---
order: 60
icon: question
image: ./static/faq.png
---

# FAQ

### 1. What is a Top Level Domain (TLD)?

A top-level domain is what some people call a domain *extension*. In the traditional world the most common TLDs are:

- `.com`
- `.org`
- `.net`
- and country TLDs like `.de`, `.es`, `.co.uk`, etc.

In the blockchain world we have our own TLDs, the most well-known is `.eth` by ENS.

Punk Domains has introduced many new TLDs to the web3 world, some of them are:

- `.op`
- `.gnosis`
- `.wagmi`
- `.ape`
- `.xdai`
- ... and many more.

### 2. What is a domain name?

Domain name is the "middle" part of a domain (between the top-level domain and the subdomain parts).

For example, if you have a domain called `techie.wagmi`, the domain name is `techie` (and `.wagmi` is a top-level domain or TLD).

### 3. How can I use a domain? Will it replace my public wallet address? 

The main purpose for blockchain domains is to be a "shortcut" for your address.

Crypto addresses are hard to remember. Ethereum-style addresses start with `0x`, and continue with 40 random characters (digits from `0` to `9` and letters from `a` to `f`).

Having a domain name provides an easy to remember shortcut for your address. If wallet supports domains, then you can enter a domain as a token receiver, and wallet will check (in the background) which address this domain is connected with.

Blockchain domains can also have other use cases. They can be **usernames** in crypto games and web3 social networks or chat apps. They can also hold many other (optional) data like a profile picture (PFP), subdomains, other addresses, email addresses etc. ([more info on custom data here](/contracts/custom-data.md)).

### 4. Can I use a domain to directly interact with wallets like MetaMask? 

Punk Domains is not yet supported on MetaMask or other wallet providers, but we're already in talks with some of them to integrate Punk Domains. 

In the mean time, you can use domains to send tokens through the Send Tokens page on the Punk Domains website.

### 5. How is this different to ENS? 

Punk Domains is an alternative to ENS. But what makes it different is a) support for multiple crypto TLDs (like .wagmi, .optimism, .ape, etc.) and b) being deployed on four different blockchains (Polygon, Arbitrum, Optimism, Gnosis Chain).

Because Punk Domains is present on L2s and sidechains, it makes minting domains, and doing other actions such as updating data and transfering domains, much cheaper than doing the same actions with ENS on L1.

### 6. Who can own a TLD? 

A top-level domain (TLD, or domain extension) can be owned by anyone. The owner of the TLD can enable/disable public domain minting, can set domain price, and earns proceeds from domain mintings. 

### 7. Is ownership of a TLD permanent? 

Currently, TLD ownership is permanent (of course, an owner can transfer ownership to another address). In the future we'll add ability to have renewable TLDs or to lend a TLD.

### 8. How long is a TLD valid for once minted? 

A TLD is valid forever.

### 9. How to mint a TLD? 

The Punk Domains governance (right now it's centralized) can decide whether anyone can mint a TLD (for a price), or not. Right now public minting is disabled, so new TLDs can only be created by the governance.

### 10. What is the cost to mint a TLD? 

Currently, public minting of a TLD is disabled. In order to get a TLD, please reach out to us via Discord.

### 11. Is ownership of a domain name permanent? 

Domain ownership is permanent. In the future we'll develop additional features that will allow for renewable domains, or to lend a domain (similar as with TLDs).

### 12. How long is a domain name valid for once minted? 

A minted domain name is valid forever.

### 13. How to mint a domain name? 

The easiest way to mint a domain is through the Punk Domains website (on the home page). 

But you can also do it through a block explorer like PolygonScan, ArbiScan, Optimism Etherscan, and Blockscout. TLD contracts are verified on all these block explorers, which means you can use the UI that they provide for interacting with smart contracts.

### 14. What are the supported blockchains? 

The supported blockchains are (by alphabetical order):

- Arbitrum One
- Gnosis Chain
- Optimism
- Polygon PoS Chain

### 15. Will there be support for non EVM compatible chains like Solana? 

We are currently not planning to support non-EVM chains.

### 16. What is the cost to mint a domain name? 

Domain prices are set by TLD owners (for each TLD separately).

### 17. Can I send tokens to a domain name? 

Yes, currently this is only possible through the Punk Domains website (see the Send Tokens page). We are working with 3rd party wallets to integrate support for Punk Domains.

### 18. Can I send NFTs to a domain name? 

Currently, only sending selected ERC-20 tokens is supported, but we will soon enable other transfers such as sending NFTs (ERC-721 and ERC-1155).

### 19. What happens if I send tokens/ NFTs to a domain name that is not minted? 

This is not possible, because a non-minted domain's "holder" is the 0x0 address, and our front-end does not allow sending tokens to the 0x0 address. If you enter a non-existing domain into the Send Tokens page, you'll receive an error (and no transaction will be made).

### 20. Can I transfer ownership of a minted TLD or Domain? 

Yes.

### 21. Will there be a marketplace for minted domain names?

This is in our roadmap, yes.

### 22. A friend has minted a domain using my referral link, but I can't see the referral fee anywhere...

Make sure to **check your address on all chains** where Punk Domains is present (at the time of writing this answer it's Polygon, Gnosis Chain, Optimism, and Arbitrum).

The referral fee is always paid out on the chain where the referred person buys the domain. Also, the referral fee transaction will show up in the **Internal Transactions** section on block explorer.
