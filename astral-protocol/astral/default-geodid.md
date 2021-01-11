# Default GeoDID



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
    "service": [{
        "id": "did:geo:123456789abcdefghi#london-congestion-zone",
        "type": "ZoneGeometryService",
        "serviceEndpoint": "https://www.url.io"
      }
    ]
  }
]
```

