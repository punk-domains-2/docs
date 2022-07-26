---
order: 79
icon: file-symlink-file
image: ./static/how-to-integrate.jpg
---

# How to integrate Punk Domains

If you'd like to integrate Punk Domains into your web3 app, chances are the only smart contract you'll need to interact with is the [Resolver contract](/contracts/resolver.md).

Each network has their own copy of the Resolver contract. Find addresses here (proxy adddresses): https://docs.punk.domains/addresses/resolver-addresses/ 

## Usecases

Let's see some common usecases.

### A) Show user's domain name instead of their address

When user connects their wallet, a web3 app usually shows their address in the navigation bar:

![](https://raw.githubusercontent.com/tempe-techie/images/main/wallet-no-domain.png)

You can check if user owns a punk domain and show that instead: 

![](https://raw.githubusercontent.com/tempe-techie/images/main/wallet-with-domain.png)

To do that, you have a few different options in the Resolver contract:

A) `getDefaultDomain(address, tld)`: Get user's default domain for a specific top-level domain (for example, `.smol`)
B) `getDefaultDomains(address)`: Get user's default domains across all TLDs (multiple domains)
C) `getFirstDefaultDomain(address)`: Get the first available user's domain, no matter of which TLD it is

With options A and C you always receive at most 1 domain name back (or none). With option B, you may receive multiple user's domains, so you can then ask the user to choose the preferred one.

### B) Fetch domain metadata

To get domain's metadata, call this function in the Resolver contract:

- `getDomainTokenUri(domainName, tld)`

Note that most punk domains have metadata stored onchain, which means it's base64 encoded. In order to decode it, you can use the standard Node library called Buffer (something like `Buffer.from(metadata.substring(29), "base64")`).

See an [example here](https://github.com/punk-domains/punk-contracts/blob/f489dbd785005a2ea590d14a1c6b23e1ab6bf98e/test/resolver/proxy.test.js#L456).

### C) Show domain image

Every domain has a default image set in its metadata. Most domains have a default image stored onchain, which means that it's in the SVG format. 

In that case the image data will look something like this: `data:image/svg+xml;base64,PHN2Zy...FTkSuQmCC` (a long string).

What to do with it? The same as you do with http image links: add it into the `src` attribute of the `<img>`:

```html
<img src="data:image/svg+xml;base64,PHN2Zy...FTkSuQmCC">
```

Easy peasy. 😀

### D) Show user's custom image

Domain holder's can set up a custom image in the domain data (not metadata, but separate [custom data](/contracts/custom-data.md)!)

The custom image does not replace the default domain image in the metadata. Instead it just provides an option for domain holder to provide their custom profile picture.

This custom image resides in the custom data, which you can fetch through the Resolver contract like this:

- `getDomainData(domainName, tld)`

This call returns a JSON object, inside which you need to find the `imgAddress` key.

The `imgAddress` value can be either an `http...` URL, an `ipfs://...` link, or NFT address (`0x...`).

Which means that user's custom image can either be:

- Image stored on a web2 server (`http` URL)
- Image stored on IPFS (`ipfs` URL)
- PFP NFT stored on blockchain (`0x` address), like for example a Bored Ape NFT

If it's an http/ipfs URL, you don't need to do anything else - this URL is the custom image link.

In case it's an NFT address (meaning it starts with `0x`), you'll need to do some additional work. First check for `imgTokenId` and `imgChainId` in the custom data. Then call the `tokenURI` function of that PFP NFT contract and parse its metadata to get the image link. In addition you can also check if the user actually owns this PFP NFT (`ownerOf(tokenId)` function in the PFP NFT contract).

### E) Search by domain

Let's say you want to allow users to search by domain. Meaning that a user enters a domain name, and then your web3 app needs to find out what's the address behind that domain (the owner address).

In this case you need to call this function in the Resolver contract:

- `getDomainHolder(domainName, tld)`

The response is the address that owns the submitted domain.

## Support

If you have a question, don't hesitate to ask us [via Discord](https://discord.gg/invite/8dSrwrAQeu).