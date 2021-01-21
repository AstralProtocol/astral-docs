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

For the draft version of this specification, `<specific-identifier>` referenced above is created by computing a Keccak256 hash of the DID controller's public key concatenated with the UNIX time, `keccak256(pub_key + time)`. In future we will design a method for generated the `<geodid-specific-identifier>` that fulfills the following requirements:

* Acts as a checksum: with the GeoDID, a user can verify the integrity of the GeoDID Document;
* Use IPFS's multibase [https://github.com/multiformats/multibase](https://github.com/multiformats/multibase)
* TODO anything else? 

An example DID for the GeoDID method:

`did:geo:9H8WRbfd4K3kQ2NTxT6L2wTNyMj1ARCaVVsT5GJ87Jw2`

TODO  does this make sense?

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
TODO the Polygon will vary based on the extension I think ... what if it is a single point?  
TODO: Will we have a `collection_metadata` object for GeoDID Collections? 

4. Generate initial `did_metadata`, including the GeoDID type \(`item` or `collection`\) and the \_\_\_\_\_\_\_ \(spec\) timestamp \(TODO moment of creation?\).

5. TODO What kind of digital signature is required, if any? 

6. Assemble the document according to this schema:

```text
// GeoDID Document schema here
```

7. TODO: Does this need to be registered anywhere? Or can it be stored as a pairwise DID? How does resolution take place? Does it rely on IDX? Or some other resolver? Smart contract? etc. Check out [peer DIDs](https://identity.foundation/peer-did-method-spec/) ... oof that's a rabbit hole ... 

For example:

\[Insert Example GeoDID\]

\[ Are we going to include Ceramic in the GeoDID Method Specification? Is it possible to not build reliance on this other network in? i.e. can't people create GeoDIDs on whatever network they want? I looked at [the `did:key` method](https://w3c-ccg.github.io/did-method-key/#bib-multibase), which Mike Prorock suggested so it could be platform / blockchain agnostic ... it won't work because these DIDs can't be updated.

However, the point that GeoDIDs shouldn't be bound to a single platform is valuable and should probably be at least mentioned in the draft spec. 

so effectively: GeoDIDs can be implemented on any platform. The alpha implementation is built on Ceramic Network. This means that we probably need to specify whic network its built on in the GeoDID, so the code knows how to resolve the document - no? Or am I getting this wrong?   \]   


// pause JOHN

### Read \(Resolve\)

The GeoDID Document is built by using read only functions and events that are triggered through the IDX identity wallet. 

#### Controller Address 

Events to build the DID Document

#### Service Endpoints

### Update

The DID Document may be updated by invoking the relevant 

### Delete \(Revoke\)



## Reference Implementations

The code at [https://github.com/astraldao/astral-protocol-core](https://github.com/astraldao/astral-protocol-core) is intended to present a reference implementation of this DID method.

\[ should we call this `js-astral` as the reference implementation in TypeScript? \]  






