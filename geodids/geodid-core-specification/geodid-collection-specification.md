---
description: >-
  The Collection Specification of the GeoDID; includes the collection's fields
  for specification.
---

# GeoDID Collection Example

## The GeoDID Collection 

As of right now, the Collection extends the default GeoDID Specification without any added fields. It is up to the user to add what they deem necessary,. However, the collection must function as a DID that will reference other DID documents or URL links. The metadata added to it must reflect that. 

### Example of GeoDID Collection

```text
[
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
      "created":"2019-03-23T06:35:22Z",
      "updated":"2019-03-23T06:37:45Z",
      "description":"Collection of EU Jurisdiction Data geojson + Raster Imagery"
   },
   "service":{
      "metadata":[
         {
            "id":"did:example:123456789abcdefghi/did-item-raster#collection-metadata",
            "type":"collection-metadata",
            "rel":"self",
            "serviceEndpoint":"<cid or url>"
         }
      ],
      "links":[
         {
            "id":"did:geo:123456789abcdefghi",
            "type":"collection",
            "rel":"root",
            "linkEndpoint":"<cid or url>"
         },
         {
            "id":"did:geo:123456789abcdefghi",
            "type":"collection",
            "rel":"self",
            "linkEndpoint":"<cid or url>"
         },
         {
            "id":"did:geo:123456789abcdefghi/did-item-raster",
            "type":"sub-collection",
            "rel":"child",
            "linkEndpoint":"<cid or url>"
         },
         {
            "id":"did:geo:123456789abcdefghi/did-item-uk",
            "type":"sub-collection",
            "rel":"child",
            "linkEndpoint":"<cid or url>"
         },
         {
            "id":"did:geo:123456789abcdefghi/did-item-netherlands",
            "type":"sub-collection",
            "rel":"child",
            "linkEndpoint":"<cid or url>"
         },
         {
            "id":"did:geo:123456789abcdefghi/did-item-germany",
            "type":"sub-collection",
            "rel":"child",
            "linkEndpoint":"<cid or url>"
         }
      ]
   }
]
```

