# GeoDID Core

> We are early in developing the GeoDID spec. For now, we are focused on storing `geojson` vector spatial data structures, and `geotiff` raster data. The GeoDID specification is designed to be flexible and identify any spatial dataset in any format - even ones that haven't been developed yet.

## **Abstract**

Geographic decentralized identifiers, or GeoDIDs, are DIDs designed to identify spatial data assets **and to be compatible with any distributed ledger or network &lt;this is tricky ...?&gt;**. Spatial data has unique properties that require special treatment - the GeoDID Method Specification defines an approach in creating, reading, updating and deleting identifiers for these assets using DIDs. In creating a GeoDID, data controllers permissionlessly create irrevocable, cryptographically-verifiable identities for spatial data assets that can be useful in decentralized applications

The objective of the GeoDID is to encourage contribution to the DID specification and Linked Data Signatures to identify and ensure trustable spatial data. This will allow rapid development of extensions to these without requiring the usage of trustless infrastructures such as blockchains or other distributed systems.

The GeoDID is inspired by the [SpatioTemporal Asset Catalog \(STAC\) specification](https://stacspec.org/) and utilizes a similar linked data structure. The structure alleviates a handful of problems associated with traversing large datasets, and allows for ease of use for the end user. Spatial data assets are identified in the service endpoints of the GeoDID document. These service endpoints can be classed as either Collections or Items. Each "Collection" contains a number of child Collections or Items;  and each "Item" will contain **several service endpoints &lt;this doesn't sound right?&gt;** that dereference to geospatial data assets. This hierarchy of encapsulating linked data within the GeoDIDs will allow for user's to find or create the data/datasets that they need easily.

{% hint style="info" %}
This data model is based on the STAC specification, which was designed for cataloging spatiotemporal data assets including satellite images, UAV imagery, LIDAR scans etc. 

For the alpha version of the specification we did not consider the OGC API - Features specification, which is better optimized for representing vector spatial data. Future versions of the GeoDID Method Specification should evolve so that vector and raster data assets are identified according to the most appropriate specification - work to be done. 
{% endhint %}

### 1. GeoDID Method

The namestring that shall identify this DID method is: `geo`.

A DID that uses this method MUST begin with the following prefix: `did:geo`. Per the DID specification, this string MUST be in lowercase. The remainder of the DID after the prefix, is specified below.

### 2. Namespace Specific Identifier:

`did:geo:<geo-specific-identifier>`

All GeoDIDs are base58 encoded using the Bitcoin / IPFS alphabets of a 16-byte UUID. 

`geo-did = "did:geo:" + geo-specific-identifier  
geo-specific-identifier = new CID(0, 'dag-pb', hash, 'base58btc')   
hash = multihash(byte, sha2-256)  
byte = new TextEncoder().encode(ethereum address + UNIX Time)`

#### Namestring Generation Method

For the draft version of this specification, `<geo-specific-identifier>` referenced above is created by computing a sha2-256 multihash on the byte representation of the DID controller's ethereum address + Unix time: `multihash(ethAddress + time, sha2-256).` Then we create a new CID Block by encoding the multihash with a base58 encoding. This will return a cid that will act as the identifier for the GeoDID. 

{% hint style="info" %}
This `<geo-specific-identifier>` generation procedure achieves our design goals of enabling one Ethereum address to control multiple GeoDIDs. However, in future versions of the specification we intend to investigate the potential of encoding more information into the identifier, including a hash or checksum of the spatial data assets identified, similar to the [Ocean Protocol DID Method](https://github.com/oceanprotocol/OEPs/blob/master/7/v0.2/README.md#how-to-compute-a-did). 

However, the GeoDID identifier should not change even if GeoDID Document contents are subsequently updated by the GeoDID controller. 
{% endhint %}

#### Identifying the correct GeoDID 

The `service` array in the GeoDID will contain several references to other GeoDIDs and/or assets. The idea is that if the GeoDID is the root DID in the hierarchy, regardless of its type, then it has the base DID identifier. If the GeoDID is a sub-collection or sub-item then it is referenced via path, and if it is an asset within the sub-item's service array, then it is referenced via fragment.

**Standalone or Root GeoDIDs using the Base DID Identifier:**

`did:geo:9H8WRbfd4K3kQ2NTxT6L2wTNyMj1ARCaVVsT5GJ87Jw2`

**Paths reference other GeoDID sub-Collections or sub-Items:**

`did:geo:9H8WRbfd4K3kQ2NTxT6L2wTNyMj1ARCaVVsT5GJ87Jw2/sub-collection-A/sub-item-1`

**Fragments reference assets within the GeoDID sub-Items:**

`did:geo:9H8WRbfd4K3kQ2NTxT6L2wTNyMj1ARCaVVsT5GJ87Jw2/sub-collection-A/sub-item-1#raster-image-1`

`did:geo:9H8WRbfd4K3kQ2NTxT6L2wTNyMj1ARCaVVsT5GJ87Jw2/sub-collection-A/sub-item-1#thumbnail`

{% hint style="info" %}
In future versions of the specification we hope to incorporate spatial, temporal and other query parameter capabilities in the GeoDID fragment, so we could retrieve matching features. By incorporating this querying, filtering and masking capability many advanced spatial decentralized applications would be enabled - though technical feasibility has not be assessed.
{% endhint %}

## 3. CRUD Operation Definitions

### Create \(Register\)

In order to create a GeoDID, a method specific identifier must be created, which will be used to build the document. After the method specific identifier is created, the user will need to select the type of Document they would like to create, Collection or Item. 

#### Required Assets

* ECDSA keypair. \(for the alpha version of the specification - future versions may be agnostic to which digital signature algorithm is used\).
* Spatial data asset\(s\), or URI\(s\) resolving to spatial data asset\(s\), along with relevant metadata / attribution.
* If GeoDID Collection, some information about the relationships between the spatial data assets being identified.

#### Proof of Concept Process

1. Create Method Specific Identifier described in \(2\), above.
2. User chooses which type of GeoDID they want to create \(Collection or standalone Item\).
3. If the user decides to create a standalone Item then they just upload the assets, did-metadata information, and item-metadata they want in the DID. The GeoDID will be built, pinned on IPFS, and anchored on the Ropsten Testnet.
4. If the user decides to create a Collection then the client will build a collection GeoDID and return the GeoDID ID. The GeoDID will be built, pinned on IPFS, and anchored on the Ropsten Testnet.
5. The user will save this GeoDID ID to append children sub-collections or sub-items as children. 
6. If the user decides to add children to the sub-collection, they repeat step 4, and use the returned GeoDID ID + Collection path to append more leaf nodes.
7. If the user decides to add items to the collection, they repeat step 3, until they finish adding all items. 

In the near future, we will also create automation features to create trees, by uploading folders with files in it. We hope this will kill two birds with one stone, so the user will only need to prepare the data once, and upload it in bulk. 

### Read \(Resolve\)

In the alpha implementation of the specification a GeoDID document can be resolved by invoking the `resolve(<GeoDID ID>)` method at contract address `<0x___TBD___>` on Ethereum's Ropsten testnet. This contract method will first verify that the user has access to this GeoDID by checking to make sure that his address registered the GeoDID via the create method.  The contract will store a mapping from the user's address  to GeoDID IDs.  

Once the user has been authenticated, the contract will trigger an event that the astral-protocol-core package will be listening for. From there the geo-did-resolver will handle the rest, and dereference to the proper GeoDID Document. 

The GeoDID Document can then be parsed and analyzed by the client, or spatial data assets can be fetched from their respective service endpoints. Do note that sometimes data assets will be identified by CIDs and stored on the IPFS network, while other service endpoints may be HTTP URLs - appropriate resolution methods will be required.

**Controller Address**

Each identity always has a controller address. To check the read only contract function `identityOwner(address identity)` on the deployed version of the ERC1056 contract.

The identity controller will always have a `publicKey` with the id set as the DID with the fragment `#key` appended.

An entry is also added to the `authentication` array of the DID document with type `Secp256k1SignatureAuthentication2018`.

#### Service Endpoints

Service Endpoints are relevant in both GeoDID Controllers **&lt;Collections?&gt;**¸ and Items. It exists to list relevant relationships to and from itself. **&lt;?Each object in the&gt;** service array will contain a required link field and several  that contain the GeoDID ID, its relationship to the DID ID, and a reference link if the controller needs to dereference it. The purpose of the link field is to enables browsers and crawlers to access the sets of Items, in an organized and straightforward way. These service endpoints can also contain references to assets that are related to a specific item.  

The GeoDID Document identified by the CID can the be resolved using a browser with native IPFS support \(`ipfs://<CID>`\), or by  resolving via a gateway, like `ipfs.io/ipfs/<GeoDID Document CID>`

### Update

The DID Document may be updated by invoking the `update(<GeoDID ID>)` method at contract address `<0x_____>` on the Ropsten testnet.  

Once the address has been verified as the DID controller, an oracle function will be invoked and will trigger an off chain event to open the GeoDID Document for the user to update. When user is done updating, they can submit the update, which will compute the CID of the GeoDID Document and compare the block to the previous CID version. 

If the CIDs differ, the client will append the timestamp of the update within the GeoDID Document, recalculate the finalized CID, and will append a new Record in the astral-core-package. The updated CID will be returned via the oracle, and appends to the end of the array of GeoDID Document CIDs, meaning users can `fetchVersionHistory(<GeoDID fragment>)` and retrieve all the CIDs of historical GeoDID documents. 

### Deactivate \(Revoke\)

A GeoDID Controller can revoke access to a GeoDID by invoking the `deactivate(<GeoDID fragment>)` method. This simply sets that GeoDID's `GeoDIDActive` record to `false` - it does not remove information from the smart contract about the historical versions of the GeoDID. It does, however, mean that future attempts to resolve that GeoDID will not succeed. 

## Reference Implementations

Once we develop it, we will store code at [https://github.com/astraldao/astral-protocol-core](https://github.com/astraldao/astral-protocol-core) as a reference implementation of this DID method.  






