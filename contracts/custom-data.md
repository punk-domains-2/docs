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
  "image": {
  	"address": "url-or-nft-address",
  	"tokenId": 0 // in case of NFT address, tokenID is mandatory, otherwise it is not
  },
  "url": "https://punk.domains",
  "emails": ["user@example.com"], // possible to add multiple emails
  "twitter": ["PunkDomains"], // possible to add multiple twitter handles
  "subdomains": {
    "sandbox": { // sandbox.techie.web3 - in case I want to have a username with different data (like PFP) in the Sandbox metaverse
      "address": "0x123...",
      "pfpTokenAddress": "0x098...",
      "pfpTokenId": 22 // PFP ownership needs to be verified on front-end
    }
  },
  "chainAddresses": { // if user wants to define different addresses on different chains (only one address per chain)
    "10": "0xa5b6...",
    "100": "0xc8d9...",
    "42161": "0xe2f3...",
  }
}
```

Note that **comments should be excluded** from your custom data. They are present in the above example just to provide some more information on the structure.