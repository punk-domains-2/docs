---
order: 20
---

# Custom data

Custom data is not a separate contract. It's a string field within the Domains struct in the [TLD contract](/contracts/tld-contract.md):

```solidity
struct Domain {
	string name;
	uint256 tokenId;
	address holder;
	string data; // <-- CUSTOM DATA
}
```

The purpose of custom data is to hold an arbitrary amount of various data (stored as a stringified JSON object).

Because the custom data field is unstructured, the Punk Domains community has to define a common standard for structuring JSON data in order to avoid parsing issues.

## Custom data standard

This section holds the official standard for structuring the custom data JSON object. Note that the standard may change over time, but we'll try to make sure that changes are always backward compatible.

**Custom data JSON structure** (example for `techie.web3`):

```json
{
  "imgAddress": "url-or-nft-address", // either an HTTP url (e.g. "http://hey.com/me.jpg") or an NFT address (0xa12B3...)
  "imgTokenId": 0, // in case of NFT address, tokenID is mandatory, otherwise it is not
  "imgChainId": 137, // the chain where NFT exists on
  
  "url": "https://punk.domains",
  "email": "user@example.com",
  "twitter": "PunkDomains",
  
  "chainAddresses": { // if user wants to define different addresses on different chains (only one address per chain)
    "10": "0xa5b6...",
    "100": "0xc8d9...",
    "42161": "0xe2f3...",
  }
}
```

Note that **comments should be excluded** from your custom data. They are present in the above example just to provide some more information on the structure.