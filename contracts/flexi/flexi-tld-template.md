---
order: 28
---

# Flexi TLD contract

TLD contracts are generated dynamically by a Factory contract based on a pre-defined template.

As the name implies, Flexi TLD contract allows for more flexibility compared to the Standard TLD contract. The major difference is that domain/NFT metadata is separated into its own contract, which makes it easier to customize both metadata and domain images.

**See the Flexi TLD contract here:** https://github.com/punk-domains/punk-contracts/blob/main/contracts/factories/flexi/FlexiPunkTLD.sol

**ABI:** https://github.com/punk-domains/punk-abi/blob/main/FlexiTldAbi.json 

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

- `name`: Domain name that goes before the TLD name. For example: `techie` in `techie.wagmi`.
- `tokenId`: Each domain is an NFT, which means it has a unique token ID. ID numbers increment for every newly minted domain starting with `0`.
- `holder`: The address that owns the domain. Domain also resolves to this address.
- `data` (optional): Domain can also hold custom data in a stringified JSON object, for example: `{"url": "https://my.homepage", "image": {"address": "0x123...orUrl", "tokenId": 22}, "description": "Some text", "twitter": "@techie1239", "friends": ["0x123..."]}`.

Read more about custom data [here](custom-data.md).

> Note that in Flexi contracts the Domain struct is defined in the [IBasePunkTLD interface](https://github.com/punk-domains/punk-contracts/blob/main/contracts/interfaces/IBasePunkTLD.sol).

## Read methods

### `metadataAddress`*

The address of the smart contract that holds metadata for the domain.

```solidity
function metadataAddress() public view returns(address)
```

Output:

- Metadata contract address

### `minter`*

The address of the smart contract that is allowed to mint domains even if `buyingEnabled` is set to `false`. Useful if you want to have minting logic in a separate smart contract.

```solidity
function minter() public view returns(address)
```

Output:

- Minter contract address

### `royaltyFeeUpdater`*

The address of the entity (either EOA or a smart contract) which is allowed to update the royalty fee. Example: This can be a  multisig wallet (like Safe) where two parties need to agree on the royalty fee change.

```solidity
function royaltyFeeUpdater() public view returns(address)
```

Output:

- Royalty Fee Updater address

### `royaltyFeeReceiver`*

The address which receives a royalty fee on each domain mint.

```solidity
function royaltyFeeReceiver() public view returns(address)
```

Output:

- Royalty Fee Receiver address

### `buyingEnabled`

If this value is set to `false`, only the TLD owner can mint new domains (for free). Otherwise anyone can mint new domains (but paid).

```solidity
function buyingEnabled() public view returns(bool)
```

Output:

- Boolean value (`true` or `false`)

### `buyingDisabledForever`*

If this value is set to `false`, the TLD owner can enable or disable domain buying at any time they want. 

But if the value is set to `true`, buying domains is disabled forever, and can never be turned on again (in that case even minter and owner cannot mint new domains anymore).

```solidity
function buyingDisabledForever() public view returns(bool)
```

Output:

- Boolean value (`true` or `false`)

### `metadataFrozen`*

If this value is set to `false`, the TLD owner can change the metadata address at any time they want. 

But if the value is set to `true`, the metadata address is frozen and can never be changed again.

```solidity
function metadataFrozen() public view returns(bool)
```

Output:

- Boolean value (`true` or `false`)

### `totalSupply`

The total number of minted domains.

```solidity
function totalSupply() public view returns(uint256)
```

Output:

- The total number of minted domains

### `idCounter`*

Counter for settings token IDs. In all Flexi TLD contracts, token IDs must start with 1, not 0 (mainly to enable the burn feature to properly work).

```solidity
function idCounter() public view returns(uint256)
```

Output:

- The next token ID number

### `price`

Returns the price to mint a new domain.

```solidity
function price() public view returns(uint256)
```

Output:

- Domain price in wei


### `royalty`

For every newly minted (paid) domain name a royalty payment is taken and sent to the Royalty Fee Receiver.

Only Royalty Fee Updater can change the royalty amount.

```solidity
function royalty() public view returns(uint256)
```

Output:

- Royalty fee in bips

### `referral`

A TLD can decide to enable referral fees for each domain mint.

By default the referral fee is set to 1000 bips (10%). If the owner does not want to allow referral fees, they need to set the referral fee to 0.

```solidity
function royalty() public view returns(uint256)
```

Output:

- Referral fee in bips

### `nameMaxLength`

Returns the maximum length of a domain name.

```solidity
function nameMaxLength() public view returns(uint256)
```

Output:

- The number of characters that a domain name can have at maximum

### `domains`

Returns the domain struct data that belong to the entered domain name.

Input:

- Domain name

```solidity
function domains(string) public view returns(Domain memory)
```

Output:

- Domain struct data

### `domainIdsNames`

Returns the domain name that belongs to the entered token ID.

Input:

- Token ID

```solidity
function domainIdsNames(uint256) public view returns(string memory)
```

Output:

- Domain name

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

### `tokenURI`

This function calls the Metadata contract and gets back domain/NFT metadata (each domain is an ERC-721 NFT).

Input:

- Token ID

```solidity
function tokenURI(uint256) public view override returns (string memory)
```

Output:

- Domain metadata as string (either base64-encoded or an URL)

## Write methods

### `burn`*

This function allows the domain owner to burn the domain. A burned domain can be minted again.

Input:

- Domain name

```solidity
function burn(string calldata _domainName) external
```

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

Function to mint a new domain for a specific address (owner). Note that both TLD owner and minter can call this function even if public minting is disabled.

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

### `changeMetadataAddress`*

Owner can change the address of the metadata contract (unless metadata address is frozen forever).

```solidity
function changeMetadataAddress(address _metadataAddress) external onlyOwner
```

Input:

- `_metadataAddress`: Metadata contract address

### `changeMinter`*

Owner can change the minter address. Minter can be either an EOA address, or a contract.

```solidity
function changeMinter(address _minter) external onlyOwner
```

Input:

- `_minter`: Minter address

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

### `disableBuyingForever`*

TLD owner can stop domain minting forever. After this call, no one can mint new domains, not even owner or minter.

```solidity
function disableBuyingForever() external onlyOwner
```

Emitted events:
- `MintingDisabledForever` event

### `freezeMetadata`*

TLD owner can freeze the metadata forever. After this call, no one can change the metadata address anymore, not even the owner.

```solidity
function freezeMetadata() external onlyOwner
```

### `toggleBuyingDomains`

TLD owner can start/stop public domain minting.

```solidity
function toggleBuyingDomains() external onlyOwner
```

Emitted events:
- `DomainBuyingToggle` event

## Royalty fee methods

### `changeRoyalty`

Royalty fee updater can change the royalty fee for minting a domain. Royalty fee is in basis points (bips).

Input:

- Royalty fee in bps

```solidity
function changeRoyalty(uint256 _royalty) external
```

Emitted events:
- `TldRoyaltyChanged` event

### `changeRoyaltyFeeReceiver`*

The existing royalty fee receiver can change the royalty fee receiver address.

Input:

- Address

```solidity
function changeRoyaltyFeeReceiver(address _newReceiver) external
```

### `changeRoyaltyFeeUpdater`*

The existing royalty fee updater can change the royalty fee updater address.

Input:

- Address

```solidity
function changeRoyaltyFeeUpdater(address _newUpdater) external
```

----

*Methods marked with a star are specific for the Flexi contract. They are not obligatory for other contracts of that type.
