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
}
```

- `name`: Domain name that goes before the TLD name. For example: `techie` in `techie.web3`.
- `tokenId`: Each domain is an NFT, which means it has a unique token ID. ID numbers increment for every newly minted domain starting with `0`.
- `holder`: The address that owns the domain. Domain also resolves to this address.
- `data` (optional): Domain can also hold custom data in a stringified JSON object, for example: `{"url": "https://my.homepage", "image": {"address": "0x123...orUrl", "tokenId": 22}, "description": "Some text", "twitter": "@techie1239", "friends": ["0x123..."]}`.

Read more about custom data [here](custom-data.md).

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

### `getDomainData`

Returns the domain holder's **custom** data. Note that this is different from the `domains` call which returns all domain struct data, not just the custom data string.

Input:

- Domain name

```solidity
function getDomainData(string memory) public view returns(string memory)
```

Output:

- Domain holder's custom data as a stringified JSON object.

### `getFactoryOwner`

Returns the address that controls the TLD Factory. This address is effectively Punk Domains governance.

```solidity
function getFactoryOwner() public view returns(address)
```

Output:

- Address that owns the Factory contract

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

### `editDefaultDomain`

Through this function, a user can set one of their domains as their default domain (within the TLD that's defined by that contract, of course).

Input:

- Domain name to be set as default

```solidity
function editDefaultDomain(string calldata _domainName) external
```

Emitted events:
- `DefaultDomainChanged` event

### `editData`

Function where user can edit custom data. Thread carefully, so that data is not accidentally deleted.

Input:

- Domain name
- Data (stringified JSON object)

```solidity
function editData(string calldata _domainName, string calldata _data) external
```

Emitted events:
- `DataChanged` event

### `mint`

Function to mint a new domain for a specific address (owner). Note that TLD owner can call this function even if public minting is disabled.

Input:

- Domain name
- Domain (future) owner
- Referrer

```solidity
function mint(
    string memory _domainName,
    address _domainHolder,
    address _referrer
  ) external payable nonReentrant returns(uint256)
```

Emitted events:
- `DomainCreated` event

## Owner methods

### `changeDescription`

TLD owner can change metadata description through this function.

Input:

- Description

```solidity
function changeDescription(string calldata _description) external onlyOwner
```

### `changeNameMaxLength`

TLD owner can change max length of newly minted domain names. Does not work retroactively.

Input:

- Maximum length

```solidity
function changeNameMaxLength(uint256 _maxLength) external onlyOwner
```

### `changePrice`

TLD owner can change domain minting price.

Input:

- Price in wei

```solidity
function changePrice(uint256 _price) external onlyOwner
```

Emitted events:
- `TldPriceChanged` event

### `changeReferralFee`

TLD owner can change the referral fee. The referral fee is in basis points (0 =< fee < 5000 bps).

Input:

- Referral fee in bps

```solidity
function changeReferralFee(uint256 _referral) external onlyOwner
```

Emitted events:
- `ReferralFeeChanged` event

### `toggleBuyingDomains`

TLD owner can start/stop public domain minting.

```solidity
function toggleBuyingDomains() external onlyOwner
```

Emitted events:
- `DomainBuyingToggle` event

## Factory owner methods

### `toggleBuyingDomains`

Factory owner can change protocol royalty for minting a domain. Royalty fee is in basis points (0 =< fee < 5000 bps).

Input:

- Royalty fee in bps

```solidity
function changeRoyalty(uint256 _royalty) external
```

Emitted events:
- `TldRoyaltyChanged` event
