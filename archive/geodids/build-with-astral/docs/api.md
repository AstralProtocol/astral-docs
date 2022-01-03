---
description: API for the @astralprotocol/contracts package
---

# API

### State modifying methods&#x20;

**constructor**

Initiates the smart contract with an hardcoded uri type representing the did method (did:geo). Also initiates the msg.sender as the default admin and as a data supplier role.

```
constructor(string memory uri) public
```

**registerRole**

Registers a new user with the ability to register a spatial asset. Contract creator is hardcoded as default admin and data supplier roles.

```
function registerRole() public
```

**enableStorage**

Registers a new storage that can accept GeoDID document creation.

```
function enableStorage(bytes32 offChainStorage) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name**            | Type    | Attributes | Description                                                             |
| ------------------- | ------- | ---------- | ----------------------------------------------------------------------- |
| **offChainStorage** | bytes32 | REQUIRED   | Bytes32 representation of the off-chain storage signature to be enabled |
{% endtab %}
{% endtabs %}

**disableStorage**

Disables an existing storage.

```
function disableStorage(bytes32 offChainStorage) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name**            | Type    | Attributes | Description                                                              |
| ------------------- | ------- | ---------- | ------------------------------------------------------------------------ |
| **offChainStorage** | bytes32 | REQUIRED   | Bytes32 representation of the off-chain storage signature to be disabled |
{% endtab %}
{% endtabs %}

**registerSpatialAsset**

Registers on-chain one Spatial Asset.

```
function registerSpatialAsset (
    address owner, 
    bytes32 geoDIDId, 
    bytes32 parentGeoDIDId , 
    bytes32[] memory childrenGeoDIDIds, 
    bytes32 cid, 
    bytes32 offChainStorage, 
    uint256 geoDIDtype
) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name**              | Type       | Attributes | Description                                                                                                                                                     |
| --------------------- | ---------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **owner**             | address    | REQUIRED   | To be designated the owner of the GeoDID. Currently must be msg.sender.                                                                                         |
| **geoDIDId**          | bytes32    | REQUIRED   | GeoDID Id generated with the GeoDID creation (check @astralprotocol/core)                                                                                       |
| **parentGeoDIDId**    | bytes32    | OPTIONAL   | GeoDID Id of the parent. Must be set to 0 if no parent is to be added.                                                                                          |
| **childrenGeoDIDIDs** | bytes32\[] | OPTIONAL   | GeoDID IDs of the children. Must be set to \[] if no children are to be added.                                                                                  |
| **cid**               | bytes32    | REQUIRED   | <p></p><p>CID of the GeoDID Document generated with its creation (check @astralprotocol/core)</p>                                                               |
| **offChainStorage**   | bytes32    | REQUIRED   | Bytes32 representation of the off-chain storage signature (must be pre-approved)                                                                                |
| **geoDIDtype**        | uint256    | REQUIRED   | 0 for Collection type GeoDIDs, 1 for Item type GeoDIDs. emit SpatialAssetRegistered(owner, geoDIDId, cid, offChainStorage, geoDIDId, \_canBeParent\[geoDIDId]); |
{% endtab %}

{% tab title="Emitted Events" %}
| Event                      | Arguments                                                                                                                  | Condition                                                         |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **SpatialAssetRegistered** | address indexed to, bytes32 indexed geoDIDId, bytes32 indexed cid, bytes32 offChainStorage, bytes32 root, bool canBeParent | Successful registration of a GeoDID                               |
| **ParentAdded**            | bytes32 indexed geoDIDId, bytes32 indexed parentGeoDIDId                                                                   | If parentGeoDIDId is different than 0                             |
| **ChildrenAdded**          | bytes32 indexed geoDIDId, bytes32 indexed childrenGeoDIDId                                                                 | If the childrenGeoDIDIds array is not empty and the GeoDIDs exist |
{% endtab %}
{% endtabs %}

**addChildrenGeoDIDs**

Adds children GeoDIDs to an existing GeoDID. GeoDIDId must correspond to a GeoDID type that can be a parent (Collection or type 0).

```
function addChildrenGeoDIDs(
    bytes32 geoDIDId, 
    bytes32[] memory childrenGeoDIDIds
) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name**              | Type       | Attributes | Description                                                                                                         |
| --------------------- | ---------- | ---------- | ------------------------------------------------------------------------------------------------------------------- |
| **geoDIDId**          | bytes32    | REQUIRED   | GeoDID Id generated with the GeoDID creation and registered in the smart contract                                   |
| **childrenGeoDIDIDs** | bytes32\[] | OPTIONAL   | GeoDID IDs of the children. Must be set to \[] if no children are to be added (nothing is executed in the function) |
{% endtab %}

{% tab title="Emitted Events" %}
| Event             | Arguments                                                  | Condition                                                         |
| ----------------- | ---------------------------------------------------------- | ----------------------------------------------------------------- |
| **ChildrenAdded** | bytes32 indexed geoDIDId, bytes32 indexed childrenGeoDIDId | If the childrenGeoDIDIds array is not empty and the GeoDIDs exist |
{% endtab %}
{% endtabs %}

**addParentGeoDID**

Adds a GeoDID as a parent to an already existing GeoDID.

```
function addParentGeoDID(
	  bytes32 geoDIDId, 
    bytes32 parentGeoDIDId
) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name**           | Type    | Attributes | Description                                                               |
| ------------------ | ------- | ---------- | ------------------------------------------------------------------------- |
| **geoDIDId**       | bytes32 | REQUIRED   | GeoDID Id generated with the GeoDID creation (check @astralprotocol/core) |
| **parentGeoDIDId** | bytes32 | REQUIRED   | GeoDID Id of the parent. It must exist.                                   |
{% endtab %}

{% tab title="Emitted Events" %}
| Event           | Arguments                                                | Condition                |
| --------------- | -------------------------------------------------------- | ------------------------ |
| **ParentAdded** | bytes32 indexed geoDIDId, bytes32 indexed parentGeoDIDId | If parentGeoDIDId exists |
{% endtab %}
{% endtabs %}

**removeChildrenGeoDIDs**

Removes children GeoDIDs from a specified GeoDID.

```
function removeChildrenGeoDIDs(
    bytes32 geoDIDId, 
    bytes32[] memory childrenGeoDIDIds
) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name**              | Type       | Attributes | Description                                                                      |
| --------------------- | ---------- | ---------- | -------------------------------------------------------------------------------- |
| **geoDIDId**          | bytes32    | REQUIRED   | GeoDID Id generated with the GeoDID creation (check @astralprotocol/core)        |
| **childrenGeoDIDIds** | bytes32\[] | OPTIONAL   | GeoDID IDs of the children. Must be set to \[] if no children are to be removed. |
{% endtab %}

{% tab title="Emitted Events" %}
| Event               | Arguments                                                  | Condition                                                          |
| ------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------ |
| **ChildrenRemoved** | bytes32 indexed geoDIDId, bytes32 indexed childrenGeoDIDId | If the childrenGeoDIDIds array is not empty and the GeoDIDs exist. |
{% endtab %}
{% endtabs %}

**removeParentGeoDID**

Removes a specified parent GeoDID from a GeoDID.

```
function removeParentGeoDID(
    bytes32 geoDIDId, 
    bytes32 parentGeoDIDId
) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name**           | Type    | Attributes | Description                                                               |
| ------------------ | ------- | ---------- | ------------------------------------------------------------------------- |
| **geoDIDId**       | bytes32 | REQUIRED   | GeoDID Id generated with the GeoDID creation (check @astralprotocol/core) |
| **parentGeoDIDId** | bytes32 | REQUIRED   | GeoDID Id of the parent to remove. It must exist.                         |
{% endtab %}

{% tab title="Emitted Events" %}
| Event             | Arguments                                                    | Condition                |
| ----------------- | ------------------------------------------------------------ | ------------------------ |
| **ParentRemoved** | bytes32 indexed geoDIDId, bytes32 **indexed** parentGeoDIDId | If parentGeoDIDId exists |
{% endtab %}
{% endtabs %}

**deactivateSpatialAsset**

De-registers a spatial asset.

```
function deactivateSpatialAsset(
    bytes32 geoDIDId, 
    bytes32[] memory childrenToRemove
) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name**              | Type       | Attributes | Description                                                                      |
| --------------------- | ---------- | ---------- | -------------------------------------------------------------------------------- |
| **geoDIDId**          | bytes32    | REQUIRED   | GeoDID Id generated with the GeoDID creation (check @astralprotocol/core)        |
| **childrenGeoDIDIds** | bytes32\[] | OPTIONAL   | GeoDID IDs of the children. Must be set to \[] if no children are to be removed. |
{% endtab %}

{% tab title="Emitted Events" %}
| Event                       | Arguments                                                  | Condition          |
| --------------------------- | ---------------------------------------------------------- | ------------------ |
| **SpatialAssetDeactivated** | bytes32 indexed geoDIDId, bytes32\[] **** childrenToRemove | If geoDIDId exists |
{% endtab %}
{% endtabs %}
