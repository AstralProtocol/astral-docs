# GeoDID Core

> We are early in developing the GeoDID spec. For now, we are focused on storing `geojson` vector spatial data structures, and `geotiff` raster data. The GeoDID specification is designed to be flexible and identify any spatial dataset in any format - even ones that haven't been developed yet.

## **Abstract**

Geographic decentralized identifiers, or GeoDIDs, are DIDs designed to identify spatial data assets and to be compatible with any distributed ledger or network. Spatial data has unique properties that require special treatment - the GeoDID Method Specification defines an approach in creating, reading, updating and deleting identifiers for these assets using DIDs. In creating a GeoDID, data controllers permissionlessly create irrevocable, cryptographically-verifiable identities for spatial data assets that can be useful in decentralized applications.

The objective of the GeoDID is to encourage contribution to the DID specification and Linked Data Signatures to identify and ensure trustable spatial data. This will allow rapid development of extensions to these without requiring the usage of trustless infrastructures such as blockchains or other distributed systems.

The GeoDID is inspired by the STAC specification and utilizes a similar linked data structure. The structure alleviates a handful of problems associated with traversing large datasets, and allows for ease of use for the end user. We adopted relationship between Collections/Catalogs and Items. The general premise of these types is: each "Collection" can either contain one of the following types, sub collections or items; and each "Item" will contain several service endpoints that dereference to geo-spatial assets. This hierarchy of encapsulating linked data within the GeoDIDs will allow for user's to find or create the data/datasets that they need easily.

### Motivation

TODO

### 1. GeoDID Method

The namestring that shall identify this DID method is: `geo`

A DID that uses this method MUST begin with the following prefix: `did:geo`. Per the DID specification, this string MUST be in lowercase. The remainder of the DID after the prefix, is specified below.

### 2. Namespace Specific Identifier:

`did:<did-method>:<specific-identifier>`

All GeoDIDs are base58 encoded using the Bitcoin / IPFS alphabets of a 16-byte UUID. 

**TODO: more info here, similar to \[this\]\(**[**https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html\#namespace-specific-identifier-nsi**](https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html#namespace-specific-identifier-nsi)**\).**

#### Namestring Generation Method

For the draft version of this specification, `<specific-identifier>` referenced above is created by computing a Keccak256 hash of the DID controller's public key concatenated with the UNIX time, `keccak256(pub_key + time).` In the future we will design a method for generated the `<geodid-specific-identifier>` that fulfills the following requirements:

* Acts as a checksum: with the GeoDID, a user can verify the integrity of the GeoDID Document;
* Uses IPFS's multibase [https://github.com/multiformats/multibase](https://github.com/multiformats/multibase);
* Maybe in the DID fragment we can include information about how to resolve the GeoDID doc? Like bytes 5-10 indicate which blockchain it's stored on or something? Anticipating multi-chain scenarios ... but this is def more advanced than we need right now.

#### Identifying the correct GeoDID 

The `service` arrays in the GeoDID will contain several references to other GeoDIDs and/or assets. The idea is that if the GeoDID is the root DID in the hierarchy, regardless of its type, then it has the base DID identifier. If the GeoDID is a sub-collection or sub-item then it is referenced via path, and if it is an asset within the sub-item's service array, then it is referenced via fragment.

**Standalone or Root GeoDIDs using the Base DID Identifier:**

`did:geo:9H8WRbfd4K3kQ2NTxT6L2wTNyMj1ARCaVVsT5GJ87Jw2`

**Paths reference other GeoDID sub-Collections or sub-Items:**

`did:geo:9H8WRbfd4K3kQ2NTxT6L2wTNyMj1ARCaVVsT5GJ87Jw2/sub-collection-A/sub-item-1`

**Fragments reference assets within the GeoDID sub-Items:**

`did:geo:9H8WRbfd4K3kQ2NTxT6L2wTNyMj1ARCaVVsT5GJ87Jw2/sub-collection-A/sub-item-1#raster-image-1`

`did:geo:9H8WRbfd4K3kQ2NTxT6L2wTNyMj1ARCaVVsT5GJ87Jw2/sub-collection-A/sub-item-1#thumbnail`

## 3. CRUD Operation Definitions

### Create \(Register\)

In order to create a GeoDID, a method specific identifier must be created, which will be used to build the document. 

#### Required Assets

* ECDSA keypair. \(for the alpha version of the specification - future versions may be agnostic to which digital signature algorithm is used\).
* Spatial data asset\(s\), or URI\(s\) resolving to spatial data asset\(s\), along with relevant metadata / attribution.
* If GeoDID Collection, some information about the relationships between the spatial data assets being identified.

#### Process

1.

### Read \(Resolve\)

In the alpha implementation of the specification a GeoDID document can be resolved by invoking the `resolve(<GeoDID ID>)` method at contract address `<0x______>` on Ethereum's Ropsten testnet. This contract method will first verify that the user has access to this GeoDID by checking to make sure that his address registered the GeoDID via the create method. The contract will store a mapping from the user's address  to GeoDID IDs.  

Once the user has been authenticated, the contract will trigger an event that the astral-protocol-core package will be listening for. From there the geo-did-resolver will handle the rest, and dereference to the proper GeoDID Document. 

The GeoDID Document can then be parsed and analyzed by the client, or spatial data assets can be fetched from their respective service endpoints. Do note that sometimes data assets will be identified by CIDs and stored on the IPFS network, while other service endpoints may be HTTP URLs - appropriate resolution methods will be required.

#### Service Endpoints

Service Endpoints are relevant in both GeoDID Controllers and Items. It exists to list relevant relationships to and from itself. The service array will contain fields that contain the GeoDID ID, its relationship to the DID ID, and a reference link if the controller needs to dereference it. The purpose of the link field is to enables browsers and crawlers to access the sets of Items, in an organized and straightforward way. These service endpoints can also contain references to assets that are related to a specific item.  

The GeoDID Document identified by the CID can the be resolved using a browser with native IPFS support \(`ipfs://<CID>`\), or by  resolving via a gateway, like `ipfs.io/ipfs/<GeoDID Document CID>`

**Authentication \[WIP\]**

Not implemented yet. Still a work in progress but we will eventually add authentication features to the GeoDID, so the controller can enable selective access to certain datasets and assets. 

### Update

The DID Document may be updated by invoking the `update(<GeoDID ID>)` method at contract address `<0x_____>` on the Ropsten testnet.  

Once the address has been verified as the DID controller, an oracle function will be invoked and will trigger an off chain event to open the GeoDID Document for the user to update. When user is done updating, they can submit the update, which will compute the CID of the GeoDID Document and compare the block to the previous CID version. 

If the CIDs differ, the client will append the timestamp of the update within the GeoDID Document, recalculate the finalized CID, and will append a new Record in the astral-core-package. The updated CID will be returned via the oracle, and appends to the end of the array of GeoDID Document CIDs, meaning users can `fetchVersionHistory(<GeoDID fragment>)` and retrieve all the CIDs of historical GeoDID documents. 

### Deactivate \(Revoke\)

A GeoDID Controller can revoke access to a GeoDID by invoking the `deactivate(<GeoDID fragment>)` method. This simply sets that GeoDID's `GeoDIDActive` record to `false` - it does not remove information from the smart contract about the historical versions of the GeoDID. It does, however, mean that future attempts to resolve that GeoDID will not succeed. 



## Security Considerations

TODO

## Privacy Considerations

TODO

## Reference Implementations

The code at [https://github.com/astraldao/astral-protocol-core](https://github.com/astraldao/astral-protocol-core) is intended to present a reference implementation of this DID method.

\[ should we call this `js-astral` as the reference implementation in TypeScript? \]  






