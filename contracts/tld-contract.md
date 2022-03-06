---
order: 28
---

# TLD template contract

TLD contracts are generated dynamically by a Factory contract based on a pre-defined template.

**See the TLD contract template here:** [https://github.com/punk-domains/punk-contracts/blob/main/contracts/PunkTLD.sol](https://github.com/punk-domains/punk-contracts/blob/main/contracts/PunkTLD.sol)

## Data

### Domain struct

Each domain name is represented as a struct:

```solidity
struct Domain {
	string name;
	uint256 tokenId;
	address holder;
	string data;
	string url;
	address pfpAddress;
	uint256 pfpTokenId;
}
```

- `name`: Domain name that goes before the TLD name. For example: `techie` in `techie.web3`.
- `tokenId`: Each domain is an NFT, which means it has a unique token ID. ID numbers increment for every newly minted domain starting with `0`.
- `holder`: The address that owns the domain. Domain also resolves to this address.
- `data` (optional): Domain can also hold custom data in a stringified JSON object, for example: `{"description": "Some text", "twitter": "@techie1239", "friends": ["0x123..."]}`.
- `url` (optional): Domain holder can specify a URL that his domain redirects to for users that use Punk Domains browser extension.
- `pfpAddress` and `pfpTokenId` (optional): Domain holder can set a default profile picture (an ERC-721 NFT that they own). This is useful for third-party integrations, for example games which would use Punk Domains for user profiles.

## Read methods

### `price`

Returns the price to mint a new domain.

```solidity
function price() public view returns(uint256)
```

Output:

- Domain price in wei

### `buyingEnabled`

If this value is set to `false`, only the TLD owner can mint new domains (for free). Otherwise anyone can mint new domains (but paid).

```solidity
function buyingEnabled() public view returns(bool)
```

Output:

- Boolean value (`true` or `false`)

### `royalty`

For every newly minted (paid) domain name a royalty payment is taken and sent to Punk Domains governance.

In case a domain is created for free by TLD owner, or if royalty is set to 0, there's no royalty to be paid.

Only Punk Domains governance can change the royalty amount. Max royalty percentage is 50%.

```solidity
function royalty() public view returns(uint256)
```

Output:

- Domain royalty in wei

### `nameMaxLength`

Returns the maximum length of a domain name.

```solidity
function nameMaxLength() public view returns(uint256)
```

Output:

- The number of characters that a domain name can have at maximum

### `totalSupply`

The total number of minted domains.

```solidity
function totalSupply() public view returns(uint256)
```

Output:

- The total number of minted domains

### `defaultNames`

Returns the domain name that the holder defined as their "default" for that specific TLD.

Input:

- User address

```solidity
function defaultNames(address) public view returns(string memory)
```

This may be useful for social networks and games where user has multiple domain names under the same TLD.

Output:

- Domain name

### `domainIdsNames`

Returns the domain name that belongs to the entered token ID.

Input:

- Token ID

```solidity
function domainIdsNames(uint256) public view returns(string memory)
```

Output:

- Domain name

### `domains`

Returns the domain struct data that belong to the entered domain name.

Input:

- Domain name

```solidity
function domains(string) public view returns(Domain memory)
```

Output:

- Domain struct data


### `getDomainHolder`

Returns the domain holder's address. If no one owns the domain (yet), the returned address is the `0x0` address.

Input:

- Domain name

```solidity
function getDomainHolder(string memory) public view returns(address)
```

This is useful for checking whether a domain name has been already taken or not.

Output:

- Domain holder's address


### `getDomainPfpAddress`

Returns the domain holder's PFP address. If there's no selected PFP (yet), the returned address is the `0x0` address.

Input:

- Domain name

```solidity
function getDomainPfpAddress(string memory) public view returns(address)
```

Output:

- Domain holder's selected PFP address (important: the holder must of that NFT)

### `getDomainPfpTokenId`

Returns the domain holder's PFP token ID. If there's no selected PFP (yet), the returned integer is `0`.

Input:

- Domain name

```solidity
function getDomainPfpTokenId(string memory) public view returns(uint256)
```

Output:

- Domain holder's selected PFP token ID (important: the holder must of that NFT)

### `getDomainData`

Returns the domain holder's **custom** data. Note that this is different from the `domains` call which returns all domain struct data, not just the custom data string.

Input:

- Domain name

```solidity
function getDomainData(string memory) public view returns(string memory)
```

Output:

- Domain holder's custom data as a stringified JSON object.

### `getDomainUrl`

Returns the domain holder's selected URL. If URL is set up, then anyone who uses Punk Domains browser extension will get redirected to the designated URL.

Input:

- Domain name

```solidity
function getDomainUrl(string memory) public view returns(string memory)
```

Output:

- Domain holder's selected URL


### `tokenURI`

Returns the domain holder's default NFT image (each domain is an ERC-721 NFT).

Input:

- Token ID

```solidity
function tokenURI(uint256) public view override returns (string memory)
```

Output:

- Domain holder's selected URL

## Write methods

- TODO...

## Owner methods

- TODO...

## Factory owner methods

- TODO...
