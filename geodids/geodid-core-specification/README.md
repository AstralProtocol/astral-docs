# GeoDID Core

> We are early in developing the GeoDID spec. For now, we are focused on storing `geojson` vector spatial data structures, and `geotiff` raster data. The GeoDID specification is designed to be flexible and identify any spatial dataset in any format - even ones that haven't been developed yet.

## **Abstract**

Geographic decentralized identifiers, or GeoDIDs, are DIDs designed to identify spatial data assets and to be compatible with any distributed ledger or network. Spatial data has unique properties that require special treatment; this GeoDID Method Specification defines an approach in creating, reading, updating and deleting identifiers for these assets using DIDs. In creating a GeoDID, data controllers permissionlessly create irrevocable, cryptographically-verifiable identities for spatial data assets that can be useful in decentralized applications.



TODO @jared : Linked Data Signatures are difficult to work with when operating a server or running a local node of some distributed system / blockchain is a requirement.  
TODO @jared: The objective of GeoDID is to encourage contribution to the DID Spec and Linked Data Signatures to identify and ensure trustable spatial data, and allow rapid development of extensions to these without requiring the use of slow, complicated, types of trustless infrastructure, such as blockchains or other distributed systems.

TODO Something about how we use the STAC model of Items and Collections.

### Motivation

TODO

### 1. GeoDID Method

The namestring that shall identify this DID method is: `geo`

A DID that uses this method MUST begin with the following prefix: `did:geo`. Per the DID specification, this string MUST be in lowercase. The remainder of the DID after the prefix, is specified below.

### 2. Namespace Specific Identifier:

`did:<did-method>:<specific-identifier>`

All GeoDIDs are base58 encoded using the Bitcoin / IPFS alphabets of a 16-byte UUID. 

TODO: more info here, similar to \[this\]\([https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html\#namespace-specific-identifier-nsi](https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html#namespace-specific-identifier-nsi)\).

#### Namestring Generation Method

TODO @jared input here - or does this make sense?

For the draft version of this specification, `<specific-identifier>` referenced above is created by computing a Keccak256 hash of the DID controller's public key concatenated with the UNIX time, `keccak256(pub_key + time)`. In future we will design a method for generated the `<geodid-specific-identifier>` that fulfills the following requirements:

* Acts as a checksum: with the GeoDID, a user can verify the integrity of the GeoDID Document;
* Use IPFS's multibase [https://github.com/multiformats/multibase](https://github.com/multiformats/multibase)
* Maybe in the DID fragment we can include information about how to resolve the GeoDID doc? Like bytes 5-10 indicate which blockchain it's stored on or something? Anticipating multi-chain scenarios ... but this is def more advanced than we need right now. 
* TODO anything else? 

An example DID for the GeoDID method:

`did:geo:9H8WRbfd4K3kQ2NTxT6L2wTNyMj1ARCaVVsT5GJ87Jw2`

#### Identifying GeoDID 

TODO This section should describe how different objects in the `service` array need to be identified by the [DID fragment](https://w3c.github.io/did-core/#fragment) - so something like `did:geo:1234123412341234#asset-id`. @jared what was your thinking behind the DID path and fragments you put in the example DID Docs in Slack?   


## 3. CRUD Operation Definitions

### Create \(Register\)

In order to create a GeoDID, a method specific identifier must be created, which will be used to build the document. 

TODO: how do we build the document? 

After the document is built, it will bind to the IDX instance for that particular user, essentially storing the GeoDID in their identity wallet. The IDX instance will act as our Verifiable Data Registry for the GeoDID Documents. However, at this point, there is no requirement for there to be any interaction with the target network. 

TODO: is this ^^^ accurate? My vote is the GeoDID Core does not rely on IDX or Ceramic - am I understand this correctly? Essentially I understand the process to be:

#### Required Assets

* ECDSA keypair. \(for the alpha version of the specification - future versions may be agnostic to which digital signature algorithm is used\).
* Spatial data asset\(s\), or URI\(s\) resolving to spatial data asset\(s\), along with relevant metadata / attribution.
* If GeoDID Collection, some information about the relationships between the spatial data assets being identified.

#### Process

1. Loop through the spatial data assets to be included in the GeoDID. If they are not URLs, compute the CIDs. For each, create an object containing the `did` \(including fragment\), `extension` , and `serviceEndpoint`, like this: 

```text
      {
        "id":"did:geo:123456789abcdefghi/did-item-raster#misc",
        "type": "misc",
        "serviceEndpoint": "<cid or url>" 
      }
```

2. Generate list of objects describing `links` - TODO @jared can you describe how this works?

3. Generate initial `item_metadata` object, a GeoJSON Feature object including a Polygon containing the area enclosed by the spatial data  asset, as well as bbox and the datetime of the moment of registration.  
TODO the Polygon will vary based on the extension I think ... what if it is a single point? Or a collection of points? / what if it is difficult to get access to the underlying data, i.e. they just want to register a large file's URL?   
TODO: Will we have a `collection_metadata` object for GeoDID Collections?   
  
&gt; Question: Can we put this metadata into the service array? For some reason I get the sense that adding custom attributes to the top level of the DID Document is poor practice. Can we make it so the first object in `service` is the `did_metadata`, and the second is the `item_metadata` - then subsequent elements in the array are the assets like we have planned? [See how the Ocean Protocol DID Method Specification does it ...](https://github.com/oceanprotocol/OEPs/blob/master/7/v0.2/README.md#ddo-services)

4. Generate initial `did_metadata`, including the GeoDID type \(`item` or `collection`\) and the ISO 8601 timestamp in the format `YYYY-MM-DDThh:mm:ss.sTZD` \(eg `1997-07-16T19:20:30.45+01:00`\)

 \(TODO is this timestamp of the moment the GeoDID is created? Probs yeah?\).

5. TODO What kind of digital signature is required, if any? 

6. Assemble the document according to this schema:

```text
// GeoDID Document schema here
```

7. TODO: Does this need to be registered anywhere? Or can it be stored as a pairwise DID? How does resolution take place? Does it rely on IDX? Or some other resolver? Smart contract? etc. Check out [peer DIDs](https://identity.foundation/peer-did-method-spec/) ... oof that's a rabbit hole ... 

For example:

```text
[Insert Example GeoDID]
```

#### TODO: Questions

\[ Are we going to include Ceramic in the GeoDID Method Specification? Is it possible to not build reliance on this other network in? i.e. can't people create GeoDIDs on whatever network they want? I looked at [the `did:key` method](https://w3c-ccg.github.io/did-method-key/), which Mike Prorock suggested so it could be platform / blockchain agnostic ... it won't work because these DIDs [can't be updated](https://w3c-ccg.github.io/did-method-key/#update).

However, the point that GeoDIDs shouldn't be bound to a single platform is valuable and should probably be at least mentioned in the draft spec. 

Ideally: GeoDIDs can be implemented on any platform. The alpha implementation is built on Ceramic Network. This means that we probably need to specify which network its built on in the GeoDID, so the code knows how to resolve the document - no? Or am I getting this wrong?   \] 

My thinking is:

* Store `GeoDIDController` address in a mapping `GeoDID fragment => address controller` 
* Store an array of `GeoDID Document CID` in a mapping `GeoDID fragment => CID[] GeoDIDDocs`
* Store  `GeoDIDActive` boolean in a mapping `GeoDID fragment => boolean active`

That way we can: 

* Update the controller on chain. Any changes to a GeoDID must originate from the `GeoDIDController` address. So we can transfer ownership of the GeoDID. Possibly a step towards data tokens? 
* Track version updates on chain, and fetch the entire version history. Should the CID reference an entire GeoDID Doc or just a diff file? I have a feeling we are solving a problem someone has already solved ...
* The `GeoDIDActive` mapping is meant to enable GeoDID Controllers to delete / deactivate GeoDIDs. \(Q: can they re-activate?\) 

### Read \(Resolve\)

In the alpha implementation of the specification a GeoDID document can be resolved by invoking the `resolve(<GeoDID fragment>)` method at contract address `<0x______>` on Ethereum's Ropsten testnet. This contract stores a mapping of GeoDID fragments =&gt;  an array of GeoDID document CIDs. The last CID in the array identifies the current valid GeoDID  Document, and is the CID returned by the `resolve` method.

The GeoDID Document identified by the CID can the be resolved using a browser with native IPFS support \(`ipfs://<CID>`\), or by  resolving via a gateway, like `ipfs.io/ipfs/<GeoDID Document CID>`

The GeoDID Document can the be parsed and analyzed by the client, or spatial data assets can be fetched from their respective service endpoints. Do note that sometimes data assets will be identified by CIDs and stored on the IPFS network, while other service endpoints may be HTTP URLs - appropriate resolution methods will be required.

#### Controller Address 

TODO: @jared anything here?  

#### Service Endpoints

TODO @jared: anything here? 

### Update

The DID Document may be updated by invoking the `update(<GeoDID fragment>, <updated GeoDID CID??>)` method at contract address `<0x_____>` on the Ropsten testnet.  

The updated CID passed into the `update` method will identify the updated GeoDID Document. This appends the new CID to the end of the array of GeoDID Document CIDs, meaning users can `fetchVersionHistory(<GeoDID fragment>)` and retrieve all the CIDs of historical GeoDID documents. 

TODO @jared have you seen this pattern? Does this make sense? How do other projects do it? 

TODO: @jared - how do we validate the changes in the GeoDID Document? i.e. that certain things haven't changed, and that 

### Delete \(Revoke\)

A GeoDID Controller can revoke access to a GeoDID by invoking the `delete(<GeoDID fragment>)` method. This simply sets that GeoDID's `GeoDIDActive` record to `false` - it does not remove information from the smart contract about the historical versions of the GeoDID. It does, however, mean that future attempts to resolve that GeoDID will not succeed. 



## Security Considerations

TODO

## Privacy Considerations

TODO

## Reference Implementations

The code at [https://github.com/astraldao/astral-protocol-core](https://github.com/astraldao/astral-protocol-core) is intended to present a reference implementation of this DID method.

\[ should we call this `js-astral` as the reference implementation in TypeScript? \]  






