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
    '@context': 'https://w3id.org/did/v1',
    id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre',
    publicKey: [
      {
        id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre#controller',
        type: 'Secp256k1VerificationKey2018',
        controller: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre',
        ethereumAddress: '0x4B11B9A1582E455c2C5368BEe0FF5d2F1dd4d28e'
      }
    ],
    didmetadata: { type: 'item', created: '2021-03-12T15:56:10.937Z' },
    links: [
      {
        id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre',
        type: 'item',
        rel: 'root'
      },
      {
        id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre',
        type: 'item',
        rel: 'self'
      }
    ],
    service: [
      {
        id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre#item-metadata-1'
        type: item-metadata
        serviceEndpoint: <CID or URL>
      },
      {
        id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre#geojson-1'
        type: geojson
        serviceEndpoint: <CID or URL>
      },
      {
        id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre#geojson-2'
        type: geojson
        serviceEndpoint: <CID or URL>
      },
      {
        id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre#geotiff-1'
        type: geotiff
        serviceEndpoint: <CID or URL>
      },
      {
        id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre#json-1'
        type: json
        serviceEndpoint: <CID or URL>
      },
      {
        id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre#misc-1'
        type: misc
        serviceEndpoint: <CID or URL>
      }
    ]
  }
]
```

