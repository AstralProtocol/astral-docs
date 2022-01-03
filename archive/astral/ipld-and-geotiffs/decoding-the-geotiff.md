# Decoding the GeoTIFF

## Process to Decode GeoTIFF and Retrieve Tile

```text
// bbox that is sent from client
const request = [
    -28493.166784412522,
    4224973.143255847,
    2358.211624949061,
    4255884.5438021915
];

// convert to window to round to nearest tile size
const targetWindow: ImageMetadata = await GeoUtils.bboxtoWindow(max_window, max_bbox, request);

// Use GetGeoTile to obtain the tile that you would like
const tiff_of_tile = await getGeoTile(ipfs, cid, ires.max_Dimensions);
```

## Using IPLD to resolve tile paths

We used the [interface-ipld-format](https://github.com/ipld/interface-ipld-format#resolverresolvebinaryblob-path) to figure out the utility functions for the IPLD Blocks. The following utility function in the [js-ipld-dag-cbor](https://github.com/ipld/js-ipld-dag-cbor) package is:

`const iter = await dagCBOR.resolver.tree(block.data);` 

The iterator `iter` contained all possible paths , in the object to outline the tree. In order to access the serialized binary of the tile, we just have to use the corresponding path with its respective `/data` tag.

```text
[
  '0,0,240,240',
  '0,0,240,240/cid',
  '0,0,240,240/data',
  '0,0,240,240/window',
  '0,0,240,240/window/0',
  '0,0,240,240/window/1',
  '0,0,240,240/window/2',
  '0,0,240,240/window/3',
  '0,0,240,240/tileSize',
  '0,0,240,240/tileSize/width',
  '0,0,240,240/tileSize/height',
  ...
  ...
  '240,240,480,480',
  '240,240,480,480/cid',
  '240,240,480,480/data',
  '240,240,480,480/window',
  '240,240,480,480/window/0',
  '240,240,480,480/window/1',
  '240,240,480,480/window/2',
  '240,240,480,480/window/3',
  '240,240,480,480/tileSize',
  '240,240,480,480/tileSize/width',
  '240,240,480,480/tileSize/height',
  '480,240,514,480',
  '480,240,514,480/cid',
  '480,240,514,480/data',
  '480,240,514,480/window',
  '480,240,514,480/window/0',
  '480,240,514,480/window/1',
  '480,240,514,480/window/2',
  '480,240,514,480/window/3',
  '480,240,514,480/tileSize',
  '480,240,514,480/tileSize/width',
  '480,240,514,480/tileSize/height'
]
```

Using `resolver.resolve(binaryBlob, path)` ,another utility function, we can take one of the paths in the Array and use it to query the data we need.

`const path = '0,240,240,480/data';`

`const result = await dagCBOR.resolver.resolve(binary, path);`

If we pass in a path with a `/data` tag, the deserialized binary will represent the source raw binary of the tile.  The serialized binary data of the Tile that we encoded earlier.

```text
<Buffer 81 59 e1 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 ... 57554 more bytes>
```

We need to deserialize the binary data in order to get back the source binary. 

`const raw_binary = await dagCBOR.util.deserialize(tile_binary.value);`

```text
[
  <Buffer 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 ... 57550 more bytes>
]
```

After we get the data back to source binary we can use the binary data and some metadata in to write back into a TIFF, with [writeArrayBuffer](https://geotiffjs.github.io/geotiff.js/global.html#writeArrayBuffer):

```text
ArrayBuffer {
  [Uint8Contents]: <4d 4d 00 2a 00 00 00 08 00 18 01 00 00 03 00 00 00 01 00 f0 00 00 01 01 00 03 00 00 00 01 00 f0 00 00 01 02 00 03 00 00 00 01 00 08 00 00 01 03 00 03 00 00 00 01 00 01 00 00 01 06 00 03 00 00 00 01 00 01 00 00 01 11 00 04 00 00 00 01 00 00 03 e8 01 15 00 03 00 00 00 01 00 01 00 00 01 16 00 04 00 00 ... 58500 more bytes>,
  byteLength: 58600
}
```

