---
description: >-
  The Item Specification of the GeoDID; includes the item's fields for
  specification.
---

# GeoDID Item Example

## The GeoDID Item 

The Item extends the default GeoDID Specification. It can function as a standalone DID and does not rely on a GeoDID Collection to be referenced.

### Example of GeoDID Item

```text
[
   {
      "@context":"https://www.w3.org/ns/did/v1",
      "id":"did:geo:123456789abcdefghi/did-item-raster",
      "authentication":[
         {
            "id":"did:geo:123456789abcdefghi/did-item-raster#keys-1",
            "type":"RsaVerificationKey2018",
            "controller":"did:geo:123456789abcdefghi",
            "publicKeyPem":"-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
         }
      ],
      "did_metadata":{
         "type":"item",
         "subtype":"raster",
         "created":"2019-03-23T06:37:45Z"
      },
      "service":{
         "item-metadata":[
            {
               "id":"did:example:123456789abcdefghi/did-item-raster#item-metadata",
               "type":"item-metadata",
               "rel":"self",
               "serviceEndpoint":"<cid or url>"
            }
         ],
         "links":[
            {
               "id":"did:geo:123456789abcdefghi",
               "type":"collection",
               "rel":"root",
               "serviceEndpoint":"<cid or url>"
            },
            {
               "id":"did:geo:123456789abcdefghi",
               "type":"sub-collection",
               "rel":"parent",
               "serviceEndpoint":"<cid or url>"
            },
            {
               "id":"did:geo:123456789abcdefghi/did-item-raster",
               "type":"item",
               "rel":"self",
               "serviceEndpoint":"<cid or url>"
            }
         ],
         "assets":[
            {
               "id":"did:example:123456789abcdefghi/did-item-raster#geotiff",
               "type":"asset",
               "type":"GeoTiff",
               "serviceEndpoint":"<cid or url>"
            },
            {
               "id":"did:example:123456789abcdefghi/did-item-raster#misc",
               "type":"asset",
               "type":"misc",
               "serviceEndpoint":"<cid or url>"
            }
         ],
      }
   }
]
```

