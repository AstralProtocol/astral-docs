# GeoDID Collection Specification

```text
[
    {
      "@context": "https://www.w3.org/ns/did/v1",
      "id": "did:geo:123456789abcdefghi",
      "authentication": [
        {
          "id": "did:geo:123456789abcdefghi#keys-1",
          "type": "RsaVerificationKey2018",
          "controller": "did:geo:123456789abcdefghi",
          "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
        }
      ],
      "did_metadata":[
        {
          "type": "collection",
          "created": "2019-03-23T06:35:22Z",
          "updated": "2019-03-23T06:37:45Z",
          "description": "Collection of EU Jurisdiction Data geojson + Raster Imagery"
        }
      ],
      "links":[
        {
            "id": "did:geo:123456789abcdefghi",
            "rel": "root",
            "linkEndpoint": "<cid or url>"
        },
        {
            "id": "did:geo:123456789abcdefghi",
            "rel": "self",
            "linkEndpoint": "<cid or url>"
        },
        {
            "id": "did:geo:123456789abcdefghi/did-item-raster",
            "rel": "child",
            "linkEndpoint": "<cid or url>"
        },
        {
            "id": "did:geo:123456789abcdefghi/did-item-uk",
            "rel": "child",
            "linkEndpoint": "<cid or url>"
        },
        {
            "id": "did:geo:123456789abcdefghi/did-item-netherlands",
            "rel": "child",
            "linkEndpoint": "<cid or url>"
        },
        {
            "id": "did:geo:123456789abcdefghi/did-item-germany",
            "rel": "child",
            "linkEndpoint": "<cid or url>"
        }
      ]
    }
]
```

part2



