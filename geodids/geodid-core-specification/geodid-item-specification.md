# GeoDID Item Specification

Under construction - stay tuned! [@AstralProtocol](https://twitter.com/AstralProtocol)

Raster GeoDID Example

```text
[
  {
    "@context": "https://www.w3.org/ns/did/v1",
    "id": "did:geo:123456789abcdefghi/did-item-raster",
    "authentication": [
      {
        "id": "did:geo:123456789abcdefghi/did-item-raster#keys-1",
        "type": "RsaVerificationKey2018",
        "controller": "did:geo:123456789abcdefghi",
        "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
      }
    ],
    "did_metadata":[
      {
        "type": "item",
        "created": "2019-03-23T06:37:45Z"
      }
    ],
    "item_metadata":[
      {
        "type": "Feature",
        "bbox": [-122.59750209, 37.48803556, -122.2880486, 37.613537207],
        "geometry": {
          "type": "Polygon",
          "coordinates": [
            [
              [-122.308150179, 37.488035566],
              [-122.597502109, 37.538869539],
              [-122.576687533, 37.613537207],
              [-122.288048600, 37.562818007],
              [-122.308150179, 37.488035566]
            ]
          ]
        },
        "properties": {
          "datetime": "2016-05-03T13:21:30.040Z"
        }
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
        "rel": "parent",
        "linkEndpoint": "<cid or url>"
      },
      {
        "id": "did:geo:123456789abcdefghi/did-item-raster",
        "rel": "self",
        "linkEndpoint": "<cid or url>"
      }
    ],
    "service": [
      {
        "id":"did:example:123456789abcdefghi/did-item-raster#geotiff",
        "type": "GeoTiff",
        "serviceEndpoint": "<cid or url>" 
      },
      {
        "id":"did:example:123456789abcdefghi/did-item-raster#misc",
        "type": "misc",
        "serviceEndpoint": "<cid or url>" 
      }
    ]
  }
]
```

GeoJSON type GeoDID \(Hyperaware Example\)

```text
[
    {
      "@context": "https://www.w3.org/ns/did/v1",
      "id": "did:geo:123456789abcdefghi/did-item-uk",
      "authentication": [
        {
          "id": "did:geo:123456789abcdefghi/did-item-uk#keys-1",
          "type": "RsaVerificationKey2018",
          "controller": "did:example:123456789abcdefghi",
          "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
        }
      ],
      "did_metadata":[
        {
            "type": "item",
            "created": "2019-03-23T06:37:45Z"
        }
      ],
      "item_metadata":[
        {
            "type": "Feature",
            "jurisdictionMetadata": {
                "jurisdictionName": "United Kingdom",
                "jurisdictionAddr": "0x123456789abcdefghi",
                "ISO3": "GBR",
                "borders": null
            }
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
          "rel": "parent",
          "linkEndpoint": "<cid or url>"
        },
        {
          "id": "did:geo:123456789abcdefghi/did-item-uk",
          "rel": "self",
          "linkEndpoint": "<cid or url>"
        }
      ],
      "service": [{
          "id": "did:example:123456789abcdefghi/did-item-uk#london-congestion-zone",
          "type": "TerrestrialPolicyZoneGeometryService",
          "zoneType": ["urban", "terrestrial"],
          "name": "London Congestion Zone",
          "serviceEndpoint": "https://raw.githubusercontent.com/johnx25bd/LBL-FutureOfBlockchain2020/fetch-geometries/data/zones/london-congestion-zone.json",
          "policies": {
            "subjectDevices": ["road", "commercial"],
            "beneficiary": "0x456789123cdef...",
            "entryCharge": 0,
            "exitCharge": 0,
            "chargePerMinute": 0.15,
            "currency": "GBP",
            "alerts": [
              "0x08aslklkdsflksa93malKLlknfdlkdl3223",
              "0x0l38asLlknfdlkksa9lklkmalKddl3223sf",
              "0x0KLlknfdlkdl3223dsflksa938aslklkmal",
              "this might be where we designate access to pebble data feeds"
            ]
          }
        },
        {
          "id": "did:example:123456789abcdefghi/did-item-uk#heathrow-restricted-airspace",
          "type": "AerialialPolicyZoneGeometryService",
          "zoneType": ["urban", "aerial"],
          "name": "Heathrow Restricted Airspace",
          "serviceEndpoint": "https://raw.githubusercontent.com/johnx25bd/LBL-FutureOfBlockchain2020/fetch-geometries/data/zones/heathrow-restricted-airspace.json",
          "policies": {
            "subjectDevices": ["uav"],
            "beneficiary": "0x678912345fghi...",
            "entryCharge": 0,
            "exitCharge": 0,
            "chargePerMinute": 0,
            "currency": "GBP",
            "alerts": [
              "0xdsflksa93malK08aslklkLlknfdlkdl32",
              "0xlklkmalKddl3223sf0l38asLlknfdlkksa9",
              "0x23dsflksa938as0KLlknfdlkdl32lklkmal"
            ]
          }
        },
        {
          "id": "did:example:123456789abcdefghi/did-item-uk#port-of-southampton",
          "type": "MaritimePolicyZoneGeometryService",
          "zoneType": [
            "port",
            "maritime"
          ],
          "name": "Port of Southampton",
          "serviceEndpoint": "https://raw.githubusercontent.com/johnx25bd/LBL-FutureOfBlockchain2020/fetch-geometries/data/zones/port-of-southampton.json",
          "policies": {
            "beneficiary": "0x89123456efghi...",
            "entryCharge": 500,
            "exitCharge": 0,
            "chargePerMinute": 0,
            "currency": "GBP",
            "alerts": [
              "0xl322308aslklKLlknfdlkdlkdsflksa93ma",
              "0xfdlkddl3223sfksa9lklkmalK0l38asLlkn",
              "0xLlknfdlkdl320sflksa938aslklkmalK23d"
            ]
          }
        }
      ]
    }
]
```

