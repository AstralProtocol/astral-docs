# Encoding the GeoTIFF

Encoding the GeoTIFF

```text

```

### Tile Object 

Beforehand the GeoTIFF is tiled at different resolutions and sizes, and the binary of the image is then serialized into an IPLD Block. This block contains the serialized binary of the tile, and its respective CID \(Content Identifier\). This data is then stored into an Object that also contains the tiles respective window and size. 

### Wrapper Object wrapping Tile Object

```text
{
  '0,240,120,360': {
    window: [ 0, 240, 120, 360 ],
    cid: CID(bafyreihdsnkivmftr64zgv23aso4eseikqlqkznrcgtmkjd4hybno2nk7i),
    data: Uint8Array(14404) [
      129, 89,  56,  64,   0,  41, 33, 58,  82, 115,  41, 74,
       99, 90,  90,  58,  25,  82, 66, 82,  74,  16,  58, 74,
       74, 66,  66,  66,   0,  66, 82, 66, 115, 197, 107, 82,
      107, 90,  90, 107, 115,  82, 74, 58,  25,   0,  25,  8,
       16, 33,  25, 107,  82,  74, 99, 90, 107,  82,  49, 66,
      123, 90,  82,  58,  82, 115, 16, 25,  16,  25,   8, 33,
       41, 58, 107,  82, 123, 107, 82, 90,  25,  33,  82, 66,
       41,  0,  33,  25,  16,  25, 49, 99,  74,  58,  25, 49,
       99, 74,  74,  90,
      ... 14304 more items
    ],
    tileSize: { width: 120, height: 120 }
  },
  '120,240,240,360': {
    window: [ 120, 240, 240, 360 ],
    cid: CID(bafyreiczb6y3ogyyvxuw5jpcfuumrn7mnxwavhrvxyfn4yqkji3tw5b3ea),
    data: Uint8Array(14404) [
      129,  89,  56,  64,  66,  58,  58,   0,  25,   8,   0,  16,
        8,   8,  82,  90,  82,  25,   0,   8,  16,  58,  33,  25,
       25,  25,  41,  33,   0,   8,  16,   8,  33,  99, 156, 165,
      123, 181, 156, 140, 140, 107, 115, 123, 107, 123, 107, 107,
       90,  66, 132, 123,  99, 165, 165, 165, 132,  99,  49, 123,
      115,  90,  66,   0,   0,  25,  25,  25,  25,  33,  25,   8,
       33,  25, 107, 123,  90,  99,  90, 115, 107,  16,  25,  82,
       90, 173,  99,  58,  82,  49,  66,  99,  99,  90,  82,  99,
       41, 115,  33,  41,
      ... 14304 more items
    ],
    tileSize: { width: 120, height: 120 }
  },
  ...
}
```

### MasterDocument Output

```text
{
  '15x15': {
    '0,15,514,30': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,45,514,60': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,75,514,90': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,105,514,120': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,135,514,150': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,165,514,180': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,195,514,210': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,225,514,240': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,255,514,270': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,285,514,300': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,315,514,330': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,345,514,360': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,375,514,390': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,405,514,420': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,435,514,450': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,465,514,480': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,495,514,510': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,510,514,0': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy)
  },
  '30x30': {
    '0,30,514,60': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,90,514,120': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,150,514,180': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,210,514,240': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,270,514,300': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,330,514,360': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,390,514,420': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,450,514,480': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,510,514,515': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy)
  },
  '60x60': {
    '0,60,514,120': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,180,514,240': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,300,514,360': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,420,514,480': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,480,514,0': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy)
  },
  '120x120': {
    '0,120,514,240': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,360,514,480': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,480,514,0': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy)
  },
  '240x240': {
    '0,240,514,480': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy),
    '0,480,514,0': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy)
  },
  '480x480': {
    '0,480,514,515': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy)
  },
  '515x514': {
    '0,0,514,0': CID(bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy)
  }
}
```

### Response after the GeoTIFF is successfully Tiled and pinned to IPFS

```text
{
  cid: 'bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy',
  max_Dimensions: [
     15,  30,  60, 120,
    240, 480, 960
  ],
  window: [ 0, 0, 514, 515 ],
  bbox: [
    -28493.166784412522,
    4224973.143255847,
    2358.211624949061,
    4255884.5438021915
  ]
}
```





