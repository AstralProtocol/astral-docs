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
   '@context':'https://w3id.org/did/v1',
   id:'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre',
   publicKey: [
      {
         id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre#controller',
         type: 'Secp256k1VerificationKey2018',
         controller: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre',
         ethereumAddress: '0x4B11B9A1582E455c2C5368BEe0FF5d2F1dd4d28e'
      }
   ],
   did_metadata:{
      type:'collection',
      created:'2019-03-23T06:35:22Z',
      updated:'2019-03-23T06:37:45Z'
   },
   links:[
      {
         id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre',
         type: 'collection',
         rel: 'root'
      },
      {
         id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre',
         type: 'collection',
         rel: 'self'
      }
   ],
   service:[
      {
         id: 'did:geo:QmdDEcQbiFEY5YWvKgk2exd6XLetgfVmswZvXRgNkpehre#collection-metadata'
         type: collection-metadata
         serviceEndpoint: <CID or URL>
      }
   ]
]
```

