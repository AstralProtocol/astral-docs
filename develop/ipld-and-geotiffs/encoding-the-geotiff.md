# Encoding the GeoTIFF

## Process of Tiling and Encoding GeoTIFF

```text
const url = 'http://download.osgeo.org/geotiff/samples/gdal_eg/cea.tif';
    
// First create instance of IPFS
const ipfs: IPFS = await create();
    
// Request TIFF from Endpoint
const image = await getImageFromUrl(url);

// Start the tiling and encoding process 
const ires: IResponse =  await startTile(ipfs, image);
```

## Tile Object 

Beforehand the GeoTIFF is tiled at different resolutions and sizes, and the binary of the image is then serialized into an IPLD Block. This block contains the serialized binary of the tile, and its respective CID \(Content Identifier\). This data is then stored into an Object that also contains the tiles respective window and size. 

### Wrapper Object wrapping Tile Objects

The Wrapper Object wraps the Tile Objects by row, as to act as a "key", when we need the path to pull these tiles. The Wrapper Object should be grouping them by the row \*2\(tileSize\), in order to encapsulate the scaled up version of the tile. 

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

The Master Document is the document that contains all the Rows, Tiles, and their respective Overviews. This is essentially the "IFD", except it is done with IPLD, and is stored as a JSON object. 

```text
{
  '30': {
    '480,0,514,60': CID(bafyreidslhcfyghycmpqtsvboms4623cinhtkqfctz64dvqyxw3ervo6t4),
    '480,60,514,120': CID(bafyreihmweufxt2nq3axnujiurnsgkzkejzakwvkr56fgp6tsureujrzcm),
    '480,120,514,180': CID(bafyreid7zfogsdrkl3ng22yqeny5aj7hhioph75kik7xjfxuyhvivaeave),
    '480,180,514,240': CID(bafyreidjxno5kq7riwykklict4zu7kfk5b4wycvgxlhtkwgpkgoqsgwxhi),
    '480,240,514,300': CID(bafyreigs3udscqv2mqvkmas3b6g2fy42dh3uy7orr4tvmhrfs6xneesfny),
    '480,300,514,360': CID(bafyreighxzwr3sfyzjmkdppdhengkgdf2qxqx5nbefaqkm6kp7ghqajesi),
    '480,360,514,420': CID(bafyreife3lpyz4vkvsmhlp6r46r72wkr3kxb5t4a3e3luhlzfw3rz3fbu4),
    '480,420,514,480': CID(bafyreihyexbwogtgjhk6lwt5p577ls6hcoi53ggvjb24xnh7kfmsobnphe),
    '480,480,514,515': CID(bafyreie6dflpabv3ywckcigfpkljlvvlruexpfjhzaiwv7lxz6gjqwk54q)
  },
  '60': {
    '480,0,514,120': CID(bafyreibjdiqovqvopi4owtk36iyenqe7reykkfsromy3l4fsmc6iuydd7y),
    '480,120,514,240': CID(bafyreih2jnnsgsvhjouhy5h3fpdmsahm5v545taljdgmbdruprzo2txbs4),
    '480,240,514,360': CID(bafyreicfd6cmsjc6taxx7kgw3qaol7ourfbsh57qajs6bwt333b3q5pfoi),
    '480,360,514,480': CID(bafyreiffelgsnbcl352drv7hdmlisjh3owlfut2cdmtvahcxlygdwxnvjy),
    '480,480,514,515': CID(bafyreieupxskp4jnhrva6t3wohsqn4uzgfngti74sysu3jypdsgpkkzyma)
  },
  '120': {
    '480,0,514,240': CID(bafyreiggzc74xwce3wn6je2bx5evpuun3gi7evjcbzwtkp3ck2hkzq4lmq),
    '480,240,514,480': CID(bafyreiax5o26tyun3miuvv7zsyf47cmtihinplkxjrccuiemuwmztisy74),
    '480,480,514,515': CID(bafyreib6xrt6daxw45t342miu7mk6yugso4f4sq25wtimdb4iv4omutf7e)
  },
  '240': {
    '480,0,514,480': CID(bafyreigkdgkrgpnpnqcion3vaiq72dyedq2qdkvb2sulpln4tkhefkkfb4),
    '480,480,514,515': CID(bafyreiahb7az6lnj63bfefogbp6w5vq5aczz3ouoh2aeen7zgbb2j5wzge)
  },
  '515': {
    '0,0,514,515': CID(bafyreibwt4pakge4urf63bwn2ot2juolaaayval6wlwnokt4ztc2uyisbe)
  }
}
```

### Response after the GeoTIFF is successfully Tiled and pinned to IPFS

The response after the GeoTIFF is successfully Tiled returns an Object that contains metadata related to the tiling job. 

| Field | Type | Description |
| :--- | :--- | :--- |
| cid | string | CID of the pinned MasterDoc |
| max\_Dimensions | Array&lt;number&gt; | Array of numbers used to understand the Size of each Tile |
| window  | Array&lt;number&gt; | The max window of the image. |
| bbox | Array&lt;number&gt; | The max bbox of the image. |

{% hint style="info" %}
Note that any future requests must be within the bbox or window returned in this object. If it isn't the request will be rejected. 
{% endhint %}

```text
{
  cid: 'bafyreigdmqpykrgxyaxtlafqpqhzrb7qy2rh75nldvfd4kok6gl47quzvy',
  max_Dimensions: [
    30,  60, 120,
    240, 515
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





