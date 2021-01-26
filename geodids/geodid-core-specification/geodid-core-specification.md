---
description: >-
  The Core Specification of the GeoDID; includes default fields for
  specification.
---

# GeoDID Core Specification

## Types of GeoDIDs 

There are two "types" of GeoDID Specifications under the Astral Protocol, that work together to enable structure between resources. At their core, they are both extensions of the DID and default GeoDID specification. However, they differ in their functionality and purpose, in order to enable a better user experience for all users.

**The GeoDID Collection -** A GeoDID Collection is a simple, flexible JSON file of service endpoints that provides a structure to organize and browse GeoDID Items. The collection is responsible for bundling a set of items or sub collections, by utilizing links to reference other child Collections or Items . The division of sub-collections is up to the implementor, but is generally done in order to make the end user's UX easier. 

**The GeoDID Item -** A GeoDID Item is an extension of the Default GeoDID Structure. Unlike its counterpart, the GeoDID Item is responsible for identifying a particular resources and referencing relative assets, through the service endpoints. GeoDID Items can only act as the leaves of the tree and cannot link to other items or collections. It can only reference assets like raster imagery, videos, geojson and reference linked parent DID Documents.

## Default GeoDID Structure

```text
[
   {
      "@context":"https://www.w3.org/ns/did/v1",
      "id":"did:geo:123456789abcdefghi",
      "authentication":[
         {
            "id":"did:geo:123456789abcdefghi#keys-1",
            "type":"RsaVerificationKey2018",
            "controller":"did:geo:123456789abcdefghi",
            "publicKeyPem":"-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
         }
      ],
      "did_metadata":{
            "type":"collection",
            "created":"2019-03-23T06:35:22Z"
      },
      "service":{      
         "links":[
            {
               "id":"did:geo:123456789abcdefghi",
               "type":"collection"
               "rel":"root",
               "serviceEndpoint":"<cid or url>"
            },
            {
               "id":"did:geo:123456789abcdefghi",
               "type":"collection",
               "rel":"self",
               "serviceEndpoint":"<cid or url>"
            }
         ]
      }
   }
]
```

## GeoDID Default Fields

| Field  | Type  | Description |
| :--- | :--- | :--- |
| id | string | **REQUIRED** The identifier for the DID Document. It can be the root DID ID or it can be a DID URL with a specific path or fragment. The id must be of the following format: did:&lt;method&gt;:&lt;specific identifier&gt;. The path\(.../path\), query\(...?query\), and fragment\(...\#fragment\) are optional but will be used later as identifiers for the children collections and items. |
| authentication | \[Authentication Object\] | **OPTIONAL BY DEFAULT** Authentication is a process \(typically some type of protocol\) by which an entity can prove it has a specific attribute or controls a specific secret using one or more [verification methods](https://www.w3.org/TR/did-core/#dfn-verification-method). With [DIDs](https://www.w3.org/TR/did-core/#dfn-decentralized-identifiers), a common example would be proving control of the private key associated with a public key published in a [DID document](https://www.w3.org/TR/did-core/#dfn-did-documents). |
| did\_metadata | did\_metadata Object | **REQUIRED** The did\_metadata object contains relative metadata pertaining to the particular GeoDID. For example, timestamps for the CRUD operations, the type of GeoDID, descriptions, etc. |
| service | Service Object  | **REQUIRED** The service object contains several sub fields used to reference metadata, other GeoDIDs, and/or assets. |

## Authentication Object Fields

The `authentication` [verification relationship](https://www.w3.org/TR/did-core/#dfn-verification-relationship) is used to specify how the [DID subject](https://www.w3.org/TR/did-core/#dfn-did-subjects) is expected to be authenticatedField, such as performing CRUD operations on the DID Document. However, the Authentication Object is optional by default as stated by the [W3C working groups' DID specification](https://www.w3.org/TR/did-core/#authentication).

| Field | Description |  |
| :--- | :--- | :--- |
| id | string |  |
| type | string |  |
| controller | string |  |
| publicKeyPem | string |  |

## DID\_Metadata Object Fields

| Field  | Type | Description |
| :--- | :--- | :--- |
| type | string | **REQUIRED** The type can either be a Collection or Item. **** |
| subtype | string  | **REQUIRED** The subtype can either be a GeoJSON or Raster. |
| created | string | **REQUIRED UPON CREATION** The geodid package will automatically timestamp the GeoDID upon creation. |
| updated  | string | **REQUIRED UPON UPDATE** The geodid package will automatically timestamp the GeoDID upon an update. If the GeoDID Document never updates then there will not be a  |
| description | string | **OPTIONAL** A description describing the GeoDID Document. It can be anything but most likely the description will address the DID subject.  |

## Service Endpoint Object Fields

, or traditional specifications /assets like geoJson, STAC, etc.

| Field  | Type | Description |
| :--- | :--- | :--- |
| metadata | \[Metadata Object\] | **OPTIONAL** The Metadata Object array will contain an array of Metadata related to the assets or links within the GeoDID. \(ex. List of Spatial Data Providers who provided the data, GeoJSON Feature\) |
| links | \[Links Object\] | **REQUIRED** The Links Object array will contain the relationships to parent and child GeoDIDs. |
| assets | \[Assets Object\]  | **OPTIONAL** The Assets Object array will contain a list of references to assets relative to the GeoDID Item.  |

### Metadata Field

| Field | Type  | Description |
| :--- | :--- | :--- |
| id | string | **REQUIRED** The DID URL that dereferences to the entity's metadata. \[\#metadata\] |
| type | string | **REQUIRED** The type of metadata. \(ex. collection-metadata, item-metadata\) |
| serviceEndpoint | string | **REQUIRED** The actual link in the format of an URL or CID. Relative and absolute links are both allowed. |

### Links Field 

This object list describes the one-to-many relationships with other GeoDIDs. These entities can be sub-collection or sub-item GeoDIDs. This object field will come in handy when a user needs to traverse or scrape a data collection.

| Field | Type | Description |
| :--- | :--- | :--- |
| id  | string | **REQUIRED** The DID URL that dereferences to the entity's GeoDID Document. This field is required if you want to create a hierarchy of GeoDID Documents \(ex. GeoDID collection is parent to GeoDID Items or Collections\).  |
| type | string | **REQUIRED** See chapter "Endpoint types" for more information. |
| rel  | string | **REQUIRED** Relationship between the current document and the linked document. See chapter "Relation types" for more information. |
| serviceEndpoint | string | **REQUIRED** The actual link in the format of an URL or CID. Relative and absolute links are both allowed. |

### Assets Field 

The Assets object list contains all the assets the GeoDID Item will need to reference. Keep in mind that GeoDID Collections will not have the assets field because they will not be referencing "Assets", their job is to reference Items that will contain the assets they need.

| Field | Type | Description |
| :--- | :--- | :--- |
| id | string | **REQUIRED** The DID URL that dereferences to the entity's asset. \[\#asset\] |
| type | string | **REQUIRED** The type of the asset. \(ex. GeoTIFF, geoJSON, PNG, CSV\) |
| serviceEndpoint | string | **REQUIRED** The actual link in the format of an URL or CID. Relative and absolute links are both allowed. |

