---
description: API for the @astralprotocol/contracts package
---

# API

### State modifying methods 

**constructor**

Initiates the smart contract with an hardcoded uri type representing the did method \(did:geo\). Also initiates the msg.sender as the default admin and as a data supplier role.

```text
constructor(string memory uri) public
```

**registerRole**

Registers a new user with the ability to register a spatial asset. Contract creator is hardcoded as default admin and data supplier roles.

```text
function registerRole() public
```

**enableStorage**

Registers a new storage that can accept GeoDID document creation.

```text
function enableStorage(bytes32 offChainStorage) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name** | Type  | Attributes | Description |
| :--- | :--- | :--- | :--- |
| **offChainStorage** | bytes32 | REQUIRED | Bytes32 representation of the off-chain storage signature to be enabled |
{% endtab %}
{% endtabs %}

**disableStorage**

Disables an existing storage.

```text
function disableStorage(bytes32 offChainStorage) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name** | Type  | Attributes | Description |
| :--- | :--- | :--- | :--- |
| **offChainStorage** | bytes32 | REQUIRED | Bytes32 representation of the off-chain storage signature to be disabled |
{% endtab %}
{% endtabs %}

**registerSpatialAsset**

Registers on-chain one Spatial Asset.

```text
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
<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Name</b>
      </th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Attributes</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>owner</b>
      </td>
      <td style="text-align:left">address</td>
      <td style="text-align:left">REQUIRED</td>
      <td style="text-align:left">To be designated the owner of the GeoDID. Currently must be msg.sender.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>geoDIDId</b>
      </td>
      <td style="text-align:left">bytes32</td>
      <td style="text-align:left">REQUIRED</td>
      <td style="text-align:left">GeoDID Id generated with the GeoDID creation (check @astralprotocol/core)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>parentGeoDIDId</b>
      </td>
      <td style="text-align:left">bytes32</td>
      <td style="text-align:left">OPTIONAL</td>
      <td style="text-align:left">GeoDID Id of the parent. Must be set to 0 if no parent is to be added.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>childrenGeoDIDIDs</b>
      </td>
      <td style="text-align:left">bytes32[]</td>
      <td style="text-align:left">OPTIONAL</td>
      <td style="text-align:left">GeoDID IDs of the children. Must be set to [] if no children are to be
        added.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>cid</b>
      </td>
      <td style="text-align:left">bytes32</td>
      <td style="text-align:left">REQUIRED</td>
      <td style="text-align:left">
        <p></p>
        <p>CID of the GeoDID Document generated with its creation (check @astralprotocol/core)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>offChainStorage</b>
      </td>
      <td style="text-align:left">bytes32</td>
      <td style="text-align:left">REQUIRED</td>
      <td style="text-align:left">Bytes32 representation of the off-chain storage signature (must be pre-approved)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>geoDIDtype</b>
      </td>
      <td style="text-align:left">uint256</td>
      <td style="text-align:left">REQUIRED</td>
      <td style="text-align:left">0 for Collection type GeoDIDs, 1 for Item type GeoDIDs. emit SpatialAssetRegistered(owner,
        geoDIDId, cid, offChainStorage, geoDIDId, _canBeParent[geoDIDId]);</td>
    </tr>
  </tbody>
</table>
{% endtab %}

{% tab title="Emitted Events" %}
| Event | Arguments | Condition |
| :--- | :--- | :--- |
| **SpatialAssetRegistered** | address indexed to, bytes32 indexed geoDIDId, bytes32 indexed cid, bytes32 offChainStorage, bytes32 root, bool canBeParent | Successful registration of a GeoDID |
| **ParentAdded** | bytes32 indexed geoDIDId, bytes32 indexed parentGeoDIDId | If parentGeoDIDId is different than 0 |
| **ChildrenAdded** | bytes32 indexed geoDIDId, bytes32 indexed childrenGeoDIDId | If the childrenGeoDIDIds array is not empty and the GeoDIDs exist |
{% endtab %}
{% endtabs %}

**addChildrenGeoDIDs**

Adds children GeoDIDs to an existing GeoDID. GeoDIDId must correspond to a GeoDID type that can be a parent \(Collection or type 0\).

```text
function addChildrenGeoDIDs(
    bytes32 geoDIDId, 
    bytes32[] memory childrenGeoDIDIds
) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name** | Type  | Attributes | Description |
| :--- | :--- | :--- | :--- |
| **geoDIDId** | bytes32 | REQUIRED | GeoDID Id generated with the GeoDID creation and registered in the smart contract |
| **childrenGeoDIDIDs** | bytes32\[\] | OPTIONAL | GeoDID IDs of the children. Must be set to \[\] if no children are to be added \(nothing is executed in the function\) |
{% endtab %}

{% tab title="Emitted Events" %}
| Event | Arguments | Condition |
| :--- | :--- | :--- |
| **ChildrenAdded** | bytes32 indexed geoDIDId, bytes32 indexed childrenGeoDIDId | If the childrenGeoDIDIds array is not empty and the GeoDIDs exist |
{% endtab %}
{% endtabs %}

**addParentGeoDID**

Adds a GeoDID as a parent to an already existing GeoDID.

```text
function addParentGeoDID(
	  bytes32 geoDIDId, 
    bytes32 parentGeoDIDId
) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name** | Type  | Attributes | Description |
| :--- | :--- | :--- | :--- |
| **geoDIDId** | bytes32 | REQUIRED | GeoDID Id generated with the GeoDID creation \(check @astralprotocol/core\) |
| **parentGeoDIDId** | bytes32 | REQUIRED | GeoDID Id of the parent. It must exist. |
{% endtab %}

{% tab title="Emitted Events" %}
| Event | Arguments | Condition |
| :--- | :--- | :--- |
| **ParentAdded** | bytes32 indexed geoDIDId, bytes32 indexed parentGeoDIDId | If parentGeoDIDId exists |
{% endtab %}
{% endtabs %}

**removeChildrenGeoDIDs**

Removes children GeoDIDs from a specified GeoDID.

```text
function removeChildrenGeoDIDs(
    bytes32 geoDIDId, 
    bytes32[] memory childrenGeoDIDIds
) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name** | Type  | Attributes | Description |
| :--- | :--- | :--- | :--- |
| **geoDIDId** | bytes32 | REQUIRED | GeoDID Id generated with the GeoDID creation \(check @astralprotocol/core\) |
| **childrenGeoDIDIds** | bytes32\[\] | OPTIONAL | GeoDID IDs of the children. Must be set to \[\] if no children are to be removed. |
{% endtab %}

{% tab title="Emitted Events" %}
| Event | Arguments | Condition |
| :--- | :--- | :--- |
| **ChildrenRemoved** | bytes32 indexed geoDIDId, bytes32 indexed childrenGeoDIDId | If the childrenGeoDIDIds array is not empty and the GeoDIDs exist. |
{% endtab %}
{% endtabs %}

**removeParentGeoDID**

Removes a specified parent GeoDID from a GeoDID.

```text
function removeParentGeoDID(
    bytes32 geoDIDId, 
    bytes32 parentGeoDIDId
) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name** | Type  | Attributes | Description |
| :--- | :--- | :--- | :--- |
| **geoDIDId** | bytes32 | REQUIRED | GeoDID Id generated with the GeoDID creation \(check @astralprotocol/core\) |
| **parentGeoDIDId** | bytes32 | REQUIRED | GeoDID Id of the parent to remove. It must exist. |
{% endtab %}

{% tab title="Emitted Events" %}
| Event | Arguments | Condition |
| :--- | :--- | :--- |
| **ParentRemoved** | bytes32 indexed geoDIDId, bytes32 **indexed** parentGeoDIDId | If parentGeoDIDId exists |
{% endtab %}
{% endtabs %}

**deactivateSpatialAsset**

De-registers a spatial asset.

```text
function deactivateSpatialAsset(
    bytes32 geoDIDId, 
    bytes32[] memory childrenToRemove
) public
```

{% tabs %}
{% tab title="Parameters" %}
| **Name** | Type  | Attributes | Description |
| :--- | :--- | :--- | :--- |
| **geoDIDId** | bytes32 | REQUIRED | GeoDID Id generated with the GeoDID creation \(check @astralprotocol/core\) |
| **childrenGeoDIDIds** | bytes32\[\] | OPTIONAL | GeoDID IDs of the children. Must be set to \[\] if no children are to be removed. |
{% endtab %}

{% tab title="Emitted Events" %}
| Event | Arguments | Condition |
| :--- | :--- | :--- |
| **SpatialAssetDeactivated** | bytes32 indexed geoDIDId, bytes32\[\] ****childrenToRemove | If geoDIDId exists |
{% endtab %}
{% endtabs %}

