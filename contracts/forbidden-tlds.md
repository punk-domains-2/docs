---
order: 31
---

# Forbidden and already-used TLDs contract

The Punk Domains architecture allows for multiple TLD factories (each with a different business model). In order to avoid colisions (two factories must not issue the same TLD), a separate contract is needed which keeps track of already-used and forbidden TLD names.

**Contract code:** [https://github.com/punk-domains-2/punk-contracts/blob/main/contracts/PunkForbiddenTlds.sol](https://github.com/punk-domains-2/punk-contracts/blob/main/contracts/PunkForbiddenTlds.sol)

## Read methods

### `isTldForbidden`

The function tells you whether a TLD name has already been used or is forbidden to use (like `.eth`), or not. If not, a TLD Factory can create it.

```solidity
function isTldForbidden(string memory _name) public view returns (bool)
```

Input:

- TLD name (for example: `.wagmi`)

Output:

- Boolean (`true` or `false`)

### `factoryAddresses`

This function returns whether a certain address has been whitelisted (as a factory address), or not.

```solidity
function factoryAddresses(address) public view returns (bool)
```

Input:

- TLD address

Output:

- Boolean (`true` or `false`)

## Owner methods

### `addForbiddenTld`

Contract owner (Punk Domains governance) can add a TLD name which can't be used by any TLD Factory for TLD registration.

```solidity
function ownerAddForbiddenTld(string memory _name) public onlyOwner
```

Input:

- `_name`: a TLD name (for example, `.eth`)

### `removeForbiddenTld`

Contract owner (Punk Domains governance) can remove a TLD name from the forbidden list.

```solidity
function removeForbiddenTld(string memory _name) public onlyOwner
```

Input:

- `_name`: a TLD name (for example, `.eth`)

### `addFactoryAddress`

Contract owner (Punk Domains governance) can add a new TLD Factory address. Every whitelisted TLD Factory can add TLD names to the forbidden list.

```solidity
function addFactoryAddress(address _fAddr) public onlyOwner
```

Input:

- `_fAddr `: a TLD factory address

### `removeFactoryAddress`

Contract owner (Punk Domains governance) can remove an existing TLD Factory address.

```solidity
function removeFactoryAddress(address _fAddr) public onlyOwner
```

Input:

- `_fAddr `: a TLD factory address
