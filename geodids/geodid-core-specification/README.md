# GeoDID Core

> We are early in developing the GeoDID spec. For now, we are focused on storing `geojson` vector spatial data structures, and `geotiff` raster data. The GeoDID specification is designed to be flexible and identify any spatial dataset in any format - even ones that haven't been developed yet.

## **Abstract**

[Decentralized Identifiers \(DIDs\)](https://w3c.github.io/did-core/) are globally-unique identifiers that 

Geographic decentralized identifiers, or GeoDIDs, are DIDs designed to identify spatial data assets. Spatial data has unique properties that require special treatment; this GeoDID Method Specification defines an approach in creating, reading, updating and deleting identifiers for these assets using DIDs. 



designed to be compatible with any distributed ledger or network. The GeoDID method is meant to make working with DIDs very simple when trusting Spatial Data Providers for assisting in resolving DID Documents \(geotiff files and geojson files within datasets\). **\[this is a bit misleading - GeoDIDs will be used by spatial data providers - but that**   


Linked Data Signatures are difficult to work with when operating a server or running a local node of some distributed system / blockchain is a requirement.  


The objective of GeoDID is to encourage contribution to the DID Spec and Linked Data Signatures to identify and ensure trustable spatial data, and allow rapid development of extensions to these without requiring the use of slow, complicated, types of trustless infrastructure, such as blockchains or other distributed systems.  


Each DID method follows the same basic format for a string identifier:

did:&lt;did-method&gt;:&lt;unique-string&gt;  


An example DID for the GeoDID method:

did:geo:&lt;specific-identifier&gt;  


## **DID Method Name**

The namestring that shall identify this DID method is: `geo`

A DID that uses this method MUST begin with the following prefix: `did:geo`. Per the DID specification, this string MUST be in lowercase. The remainder of the DID after the prefix, is specified below.

### Method Specific Identifier 

The method specifier identifier is represented as a hash that is derived from the public key of the DID controller. 

\[

\*show example of how it is hashed and explain further

* What digital signature algorithm is used for GeoDIDs? Or any? 
* Also, if it is deterministically calculated from the public key, that means each account can only create one GeoDID. It probably should be created from `hash(publicKey, spatialDataAsset)` - that way the same account could create multiple GeoDIDs. I'm imagining the same account probably creating a new GeoDID for each of their universal check-ins. 

\]  


## CRUD Operation Definitions

### Create \(Register\)

In order to create a GeoDID, a method specific identifier must be created beforehand then we can build the document. After the document is built, it will bind to the IDX instance for that particular user, essentially storing the GeoDID in their identity wallet. The IDX instance will act as our Verifiable Data Registry for the GeoDID Documents. However, at this point, there is no requirement for there to be any interaction with the target network.   


\[Insert Example GeoDID\]

\[ Are we going to include Ceramic in the GeoDID Method Specification? Is it possible to not build reliance on this other network in? i.e. can't people create GeoDIDs on whatever network they want? Remembering Mike Prorock's point to be platform / blockchain agnostic ...

so effectively: GeoDIDs can be implemented on any platform. The alpha implementation is built on Ceramic Network. This means that we probably need to specify whic network its built on in the GeoDID, so the code knows how to resolve the document - no? Or am I getting this wrong?   \]   


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






