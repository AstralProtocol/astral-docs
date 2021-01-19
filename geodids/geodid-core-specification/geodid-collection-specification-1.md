---
description: >-
  The Collection Specification of the GeoDID; includes the collection's fields
  for specification.
---

# GeoDID Collection Specification

## The GeoDID Collection 

As of right now, the Collection extends the default GeoDID Specification without any added fields. It is up to the user to add what they deem necessary, however, the collection must function as a DID that will reference other DID documents or URL links. The metadata added to it must reflect that. 

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
   "link":[
      {
         "id":"did:geo:123456789abcdefghi",
         "rel":"root",
         "linkEndpoint":"<cid or url>"
      },
      {
         "id":"did:geo:123456789abcdefghi",
         "rel":"self",
         "linkEndpoint":"<cid or url>"
      },
      {
         "id":"did:geo:123456789abcdefghi/did-item-raster",
         "rel":"child",
         "linkEndpoint":"<cid or url>"
      },
      {
         "id":"did:geo:123456789abcdefghi/did-item-uk",
         "rel":"child",
         "linkEndpoint":"<cid or url>"
      },
      {
         "id":"did:geo:123456789abcdefghi/did-item-netherlands",
         "rel":"child",
         "linkEndpoint":"<cid or url>"
      },
      {
         "id":"did:geo:123456789abcdefghi/did-item-germany",
         "rel":"child",
         "linkEndpoint":"<cid or url>"
      }
   ]
]
```

## 

