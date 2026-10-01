---
description: >-
  Every class and method in the thoth.id SDK, with parameters, return values and
  examples.
icon: code
---

# SDK Reference

Start with a group, or jump to a method in the table below. Upgrading from v2? Read [Migrating from v2](sdk-reference/migrating-from-v2.md).

Install the SDK from [npm](https://www.npmjs.com/package/thoth-id-sdk) with `npm install thoth-id-sdk`. See the [Quickstart](getting-started/quickstart.md) for setup.

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="image">Cover image</th></tr></thead><tbody><tr><td><strong>Object Management</strong></td><td>Create the SDK instance and point it at a node and contract.</td><td><a href="sdk-reference/object-management/">object-management</a></td><td><a href=".gitbook/assets/sdk-group-01.jpg">sdk-group-01.jpg</a></td></tr><tr><td><strong>Name Methods</strong></td><td>Resolve, validate and inspect names and their owners.</td><td><a href="sdk-reference/name-methods/">name-methods</a></td><td><a href=".gitbook/assets/sdk-group-02.jpg">sdk-group-02.jpg</a></td></tr><tr><td><strong>Contract &#x26; Fees</strong></td><td>Fees and multipliers, plus the contract's domain, managers and profile limits.</td><td><a href="sdk-reference/fee-information/">fee-information</a></td><td><a href=".gitbook/assets/sdk-group-contract-fees.jpg">sdk-group-contract-fees.jpg</a></td></tr></tbody></table>

## Classes

### ThothIdSDK

The main class for interacting with the thoth.id nano contracts.

## Methods

| Method                                                                  | Description                                                                        |
| ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| [`constructor`](sdk-reference/constructor.md)                           | Creates a new instance of the SDK.                                                 |
| [`loadContractIds`](sdk-reference/loadContractIds.md)                   | Collects the map of domain suffixes and contract IDs from the node.                |
| [`refreshContractIds`](sdk-reference/refreshContractIds.md)             | Discards the cached map and collects it again.                                     |
| [`exportContractIds`](sdk-reference/exportContractIds.md)               | Returns a copy of the cached map, to save and reuse later.                         |
| [`setContractIds`](sdk-reference/setContractIds.md)                     | Seeds the instance with a previously saved map.                                    |
| [`getDomains`](sdk-reference/getDomains.md)                             | Lists the domain suffixes the instance knows about.                                |
| [`getContractIdForDomain`](sdk-reference/getContractIdForDomain.md)     | Returns the cached contract ID of a domain suffix.                                 |
| [`setNodeUrl`](sdk-reference/setNodeUrl.md)                             | Sets the Hathor full-node URL.                                                     |
| [`setContractId`](sdk-reference/setContractId.md)                       | Sets a specific contract ID to be used for all calls.                              |
| [`setBlueprintId`](sdk-reference/setBlueprintId.md)                     | Sets the blueprint ID used to discover domain contracts.                           |
| [`isNameAvailable`](sdk-reference/isNameAvailable.md)                   | Checks if a name is available to be registered.                                    |
| [`resolveName`](sdk-reference/resolveName.md)                           | Resolves a name to its associated wallet address.                                  |
| [`getNameData`](sdk-reference/getNameData.md)                           | Retrieves the raw data associated with a name.                                     |
| [`getProfileData`](sdk-reference/getProfileData.md)                     | Retrieves the profile data associated with a name.                                 |
| [`getNameOwner`](sdk-reference/getNameOwner.md)                         | Gets the owner's address for a given name.                                         |
| [`getNameExpirationInfo`](sdk-reference/getNameExpirationInfo.md)       | Gets expiration information for a name.                                            |
| [`getNameExpirationDate`](sdk-reference/getNameExpirationDate.md)       | Gets the exact expiration date of a name.                                          |
| [`validateName`](sdk-reference/validateName.md)                         | Validates the format of a name.                                                    |
| [`checkNameOwnership`](sdk-reference/checkNameOwnership.md)             | Checks if a given address owns a name.                                             |
| [`checkNameStatus`](sdk-reference/checkNameStatus.md)                   | Checks the current status of a name (e.g., active, expired).                       |
| [`getFeeInfo`](sdk-reference/getFeeInfo.md)                             | Gets information about the fees for a name.                                        |
| [`calculateFee`](sdk-reference/calculateFee.md)                         | Calculates the registration or renewal fee for a name.                             |
| [`getFeeMultiplier`](sdk-reference/getFeeMultiplier.md)                 | Gets the fee multiplier for a name of a certain length for a given domain.         |
| [`getFeeStructure`](sdk-reference/getFeeStructure.md)                   | Retrieves the entire fee structure of a specific contract.                         |
| [`getManagerNames`](sdk-reference/getManagerNames.md)                   | Gets all names managed by a specific address on a given domain.                    |
| [`getManagerPrimaryName`](sdk-reference/getManagerPrimaryName.md)       | Gets the primary name set for a manager address on a given domain.                 |
| [`getDevAddress`](sdk-reference/getDevAddress.md)                       | Gets the developer address of the contract for a given domain.                     |
| [`getContractDomain`](sdk-reference/getContractDomain.md)               | Gets the domain of the contract (e.g., `.htr`).                                    |
| [`getGracePeriodDays`](sdk-reference/getGracePeriodDays.md)             | Gets the grace period for name renewals for a given domain.                        |
| [`getMaxProfileDataEntries`](sdk-reference/getMaxProfileDataEntries.md) | Gets the maximum number of data entries in a profile for a given domain.           |
| [`getMaxProfileKeyLength`](sdk-reference/getMaxProfileKeyLength.md)     | Gets the maximum length of a profile data key for a given domain.                  |
| [`getMaxProfileValueLength`](sdk-reference/getMaxProfileValueLength.md) | Gets the maximum length of a profile data value for a given domain.                |
| [`getMaxTokenSymbolLength`](sdk-reference/getMaxTokenSymbolLength.md)   | Gets the maximum length of a token symbol for a given domain.                      |
| [`getMaxTotalProfileSize`](sdk-reference/getMaxTotalProfileSize.md)     | Gets the maximum total size of a profile for a given domain.                       |
| [`validateKeyFormat`](sdk-reference/validateKeyFormat.md)               | Validates the format of a key-value pair for profile data for a given domain.      |
| [`callMultiple`](sdk-reference/callMultiple.md)                         | Allows making multiple view calls to a specific contract in a single request.      |
| [`callMultipleSettled`](sdk-reference/callMultipleSettled.md)           | Like callMultiple, but returns each call's own outcome.                            |
