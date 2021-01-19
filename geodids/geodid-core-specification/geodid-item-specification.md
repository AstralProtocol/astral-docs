---
description: >-
  The Item Specification of the GeoDID; includes the item's fields for
  specification.
---

# GeoDID Item Specification

## The GeoDID Item 

The Item extends the default GeoDID Specification with `item_metadata` and `service` objects added on as fields. The GeoDID Item can function as a standalone DID and does not rely on a GeoDID Collection to be referenced.

### GeoDID Item Fields

| Field | Type | Description |
| :--- | :--- | :--- |
| item\_metadata | \[item\_metadata Object\] | **REQUIRED** The ****Item Metadata Object  is responsible for  ****metadata associate with the item itself. This could be a bounding box, polygon, etc.  |
| service | \[service Object\] | **REQUIRED** The Service Object contains a list of Service Endpoints that the GeoDID can reference. These service endpoints will dereference to assets like geoTIFFs, geojsons, etc. |

### Item\_Metadata Object Fields

| Field | Type | Description |
| :--- | :--- | :--- |
|  |  |  |

### Service Object Fields 

| Field |  |  |
| :--- | :--- | :--- |
| serviceEndpoint | string | **REQUIRED** The actual link in the format of an URL or CID. Relative and absolute links are both allowed. |
| type | string | **REQUIRED** Media type of the asset. |
| id | string | **OPTIONAL** The DID URL that dereferences to the entity's GeoDID Document. This field is required if you want to create a hierarchy of GeoDID Documents \(ex. GeoDID collection is parent to GeoDID Items or Collections\).  |

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
         "created":"2019-03-23T06:37:45Z"
      },
      "item_metadata":[
         {
            "type":"Feature",
            "bbox":[
               -122.59750209,
               37.48803556,
               -122.2880486,
               37.613537207
            ],
            "geometry":{
               "type":"Polygon",
               "coordinates":[
                  [
                     [
                        -122.308150179,
                        37.488035566
                     ],
                     [
                        -122.597502109,
                        37.538869539
                     ],
                     [
                        -122.576687533,
                        37.613537207
                     ],
                     [
                        -122.288048600,
                        37.562818007
                     ],
                     [
                        -122.308150179,
                        37.488035566
                     ]
                  ]
               ]
            },
            "properties":{
               "datetime":"2016-05-03T13:21:30.040Z"
            }
         }
      ],
      "links":[
         {
            "id":"did:geo:123456789abcdefghi",
            "rel":"root",
            "linkEndpoint":"<cid or url>"
         },
         {
            "id":"did:geo:123456789abcdefghi",
            "rel":"parent",
            "linkEndpoint":"<cid or url>"
         },
         {
            "id":"did:geo:123456789abcdefghi/did-item-raster",
            "rel":"self",
            "linkEndpoint":"<cid or url>"
         }
      ],
      "service":[
         {
            "id":"did:example:123456789abcdefghi/did-item-raster#geotiff",
            "type":"GeoTiff",
            "serviceEndpoint":"<cid or url>"
         },
         {
            "id":"did:example:123456789abcdefghi/did-item-raster#misc",
            "type":"misc",
            "serviceEndpoint":"<cid or url>"
         }
      ]
   }
]
```

