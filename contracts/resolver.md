---
order: 10
---

# Resolver contract

Each TLD has in-built resolver (`getDomainHolder`) and reverse-resolver (`defaultNames`) functions. But in order to simplify resolving domains, there's also the PunkResolver contract, which can resolve all punk TLDs. 

The benefit is that you only need to store one contract address (the PunkResolver), instead of all TLD addresses.

**Contract code:** https://github.com/punk-domains/punk-contracts/tree/main/contracts/resolver

## State variables

### `isTldDeprecated` mapping

```solidity
mapping (address => bool) public isTldDeprecated;
```

Resolver owner (Punk Domains governance) can deprecate or delist a TLD. This does not mean that TLD contract is not functional anymore. It's just preventing it from being resolved through the Resolver contract. Everything else regarding the TLD contract will still work as before.

### `factories` array

```solidity
address[] public factories;
```

The array of TLD Factory contracts that this Resolver contract supports.

## Read methods

### `getDefaultDomain` (singular)

Returns the default domain for an address on a given TLD.

```solidity
function getDefaultDomain(address _addr, string calldata _tld) public view returns(string memory)
```

Input:

- `_addr`: the address of which you want to get a default domain
- `_tld`: the top-level domain in question

Output:

- The default domain name. If none, it returns an empty string.

### `getDefaultDomains` (plural)

> Note that this function name is in plural!

Returns a stringified list of default domains across all TLDs (comma-separated string).

```solidity
function getDefaultDomains(address _addr) public view returns(string memory)
```

Input:

- `_addr`: the address of which you want to get a default domain

Output:

- A list of default domain names (comma-separated string). If none, it returns an empty string.


### `getDomainHolder`

Returns the address that owns a given domain.

```solidity
function getDomainHolder(string calldata _domainName, string calldata _tld) public view returns(address)
```

Input:

- `_domainName`: the name part of the domain (like "tempe" in "tempe.wagmi")
- `_tld`: the domain extension (like ".wagmi")

Output:

- The address that owns a given domain.


### `getDomainData`

Returns the [custom data](custom-data.md) of a given domain.

```solidity
function getDomainData(string calldata _domainName, string calldata _tld) public view returns(string memory)
```

Input:

- `_domainName`: the name part of the domain (like "tempe" in "tempe.wagmi")
- `_tld`: the domain extension (like ".wagmi")

Output:

- Custom data (JSON string)


### `getDomainTokenUri`

Returns the metadata of a given domain. Note that metadata is base64 encoded, so you need to decode it first.

```solidity
function getDomainTokenUri(string calldata _domainName, string calldata _tld) public view returns(string memory)
```

Input:

- `_domainName`: the name part of the domain (like "tempe" in "tempe.wagmi")
- `_tld`: the domain extension (like ".wagmi")

Output:

- Metadata (JSON string)


### `getFactoriesArray`

Returns the array of TLD factories supported by this Resolver contract.

```solidity
function getFactoriesArray() public view returns(address[] memory)
```

Output:

- Array of factory addresses

### `getFirstDefaultDomain`

Returns a single default domain across all TLDs (the one that comes first, but was not necessarily created first).

```solidity
function getFirstDefaultDomain(address _addr) public view returns(string memory)
```

Input:

- `_addr`: the address of which you want to get a default domain

Output:

- A single domain name.

### `getTldAddress`

Fetch the address of a given top-level domain (unless it was marked as deprecated).

```solidity
function getTldAddress(string calldata _tldName) public view returns(address)
```

Input:

- `_tldName`: top-level domain name (example: ".wagmi")

Output:

- The TLD contract address

### `getTldFactoryAddress`

Fetch the address of the Factory of a given top-level domain (unless the TLD was marked as deprecated).

```solidity
function getTldFactoryAddress(string calldata _tldName) public view returns(address)
```

Input:

- `_tldName`: top-level domain name (example: ".wagmi")

Output:

- The TLD Factory contract address


### `getTlds`

Fetch a list of all (non-deprecated) TLDs and their addresses.

```solidity
function getTlds() public view returns(string memory)
```

Output:

- List of all active TLDs (stringified CSV)

## Owner methods

### `addFactoryAddress`

Resolver owner can add a factory address to the Resolver's factory array.

```solidity
function addFactoryAddress(address _factoryAddress) external onlyOwner
```

Input:

- `_factoryAddress`: TLD Factory address

### `addDeprecatedTldAddress`

Resolver owner can deprecate a TLD address. This means that the Resolver contract does not support it anymore.

```solidity
function addDeprecatedTldAddress(address _deprecatedTldAddress) external onlyOwner
```

Input:

- `_deprecatedTldAddress`: TLD address

### `removeFactoryAddress`

Resolver owner can remove a factory address from the Resolver's factory array.

```solidity
function removeFactoryAddress(uint _addrIndex) external onlyOwner
```

Input:

- `_addrIndex`: TLD Factory address index in the array

### `removeDeprecatedTldAddress`

Resolver owner can remove a TLD address from being deprecated. After that, the TLD address is not deprecated anymore and can be resolved through the Resolver contract.

```solidity
function removeDeprecatedTldAddress(address _deprecatedTldAddress) external onlyOwner
```

Input:

- `_deprecatedTldAddress`: TLD address
