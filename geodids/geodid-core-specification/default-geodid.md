# Default GeoDID

Under construction - stay tuned! [@AstralProtocol](https://twitter.com/AstralProtocol)

This document explains the structure and content of the default GeoDID. The following fields are the default fields added to the DID Document upon creation. 

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
          "type": "default",
          "created": "2019-03-23T06:35:22Z"
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
        }
      ]
    }
]
```

