---
order: 1
---

# How to integrate .flr names

.flr smart contract: [0xBDACF94dDCAB51c39c2dD50BffEe60Bb8021949a](https://flarescan.com/token/0xBDACF94dDCAB51c39c2dD50BffEe60Bb8021949a?type=erc721&chainid=14)

There are only two functions in the .flr smart contract important for integrations:
- Resolver: `getDomainHolder(name)` (note: enter only name without extension, e.g.: alice, not alice.flr)
- Reverse resolver: `defaultNames(address)`

## Resolver (getDomainHolder): get user's address

> [*Try it yourself on block explorer*](https://flarescan.com/token/0xBDACF94dDCAB51c39c2dD50BffEe60Bb8021949a/contract/readContract?chainid=14#F10)

Useful when you have a name (e.g. `tempe.flr`) and would like to learn which address is behind this name.

Note: When you enter domain name, enter only the name (e.g. `tempe` ✅) without extension (not `tempe.flr` ⛔️).

Example with ether.js:

```js
const flrNameContract = new ethers.Contract(
  "0xBDACF94dDCAB51c39c2dD50BffEe60Bb8021949a", 
  new ethers.utils.Interface(["function getDomainHolder(string calldata _domainName) public view returns(address)"]),
  provider
);

const userAddress = await flrNameContract.getDomainHolder("tempe"); // returns the address that owns tempe.flr, should be 0xb29050965A5AC70ab487aa47546cdCBc97dAE45D
```

## Reverse resolver (defaultNames): get user's .flr name
> [*Try it yourself on block explorer*](https://flarescan.com/token/0xBDACF94dDCAB51c39c2dD50BffEe60Bb8021949a/contract/readContract?chainid=14#F4)

Useful when you have an address (e.g. when user connects to your app), and you'd like to get a `.flr` name of that address.

Example with ether.js:

```js
const flrNameContract = new ethers.Contract(
  "0xBDACF94dDCAB51c39c2dD50BffEe60Bb8021949a", 
  new ethers.utils.Interface(["function defaultNames(address) public view returns(string memory)"]),
  provider
);

const userName = await flrNameContract.defaultNames("0xb29050965A5AC70ab487aa47546cdCBc97dAE45D"); // returns the .flr name

const fullFlrName = userName + ".flr"; // tempe.flr
```

## Network Configuration

When working with .flr domains, make sure your provider is connected to the Flare network:

```js
// Flare mainnet configuration
const provider = new ethers.providers.JsonRpcProvider("https://flare-api.flare.network/ext/bc/C/rpc");
// or use your preferred RPC provider for Flare network
```

## Support

If you'll have any questions regarding the integration, feel free to reach out to us via social media: https://x.com/flrdomains
