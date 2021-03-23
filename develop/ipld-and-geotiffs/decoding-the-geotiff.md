# Decoding the GeoTIFF

DAG-CBOR

Getting Started

```text
import { getImageFromUrl, startTile, getGeoTile } from "ipld-geotiff";
import { IPFS, create } from "ipfs";

async function example(){
    const url = 'http://download.osgeo.org/geotiff/samples/gdal_eg/cea.tif';
    
    // First create instance of IPFS
    const ipfs: IPFS = await create();
    
    // Request TIFF from Endpoint
    const image = await getImageFromUrl(url);
    // Start the tiling and encoding process 
    const ires: IResponse =  await startTile(ipfs, image);

    // 
    const targetWindow: ImageMetadata = await GeoUtils.bboxtoWindow(ires.window, ires.bbox, request);

    // Use GetGeoTile to obtain the tile that you would like
    const tiff_of_tile = await getGeoTile(ipfs, ires.cid, ires.max_Dimensions);
}
```

Using the Resolve function again we can see



Router

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
  '0,240,240,480',
  '0,240,240,480/cid',
  '0,240,240,480/data',
  '0,240,240,480/window',
  '0,240,240,480/window/0',
  '0,240,240,480/window/1',
  '0,240,240,480/window/2',
  '0,240,240,480/window/3',
  '0,240,240,480/tileSize',
  '0,240,240,480/tileSize/width',
  '0,240,240,480/tileSize/height',
  '240,0,480,240',
  '240,0,480,240/cid',
  '240,0,480,240/data',
  '240,0,480,240/window',
  '240,0,480,240/window/0',
  '240,0,480,240/window/1',
  '240,0,480,240/window/2',
  '240,0,480,240/window/3',
  '240,0,480,240/tileSize',
  '240,0,480,240/tileSize/width',
  '240,0,480,240/tileSize/height',
  '480,0,514,240',
  '480,0,514,240/cid',
  '480,0,514,240/data',
  '480,0,514,240/window',
  '480,0,514,240/window/0',
  '480,0,514,240/window/1',
  '480,0,514,240/window/2',
  '480,0,514,240/window/3',
  '480,0,514,240/tileSize',
  '480,0,514,240/tileSize/width',
  '480,0,514,240/tileSize/height',
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

The serialized binary data of the Tile that we encoded earlier.

```text
<Buffer 81 59 e1 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 ... 57554 more bytes>
```

We need to deserialize the binary data in order to get back the source binary. 

```text
[
  <Buffer 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 ... 57550 more bytes>
]
```

After we get the data back to source binary we can use the binary data and some metadata in to write back into a TIFF. 



```text
ArrayBuffer {
  [Uint8Contents]: <4d 4d 00 2a 00 00 00 08 00 18 01 00 00 03 00 00 00 01 00 f0 00 00 01 01 00 03 00 00 00 01 00 f0 00 00 01 02 00 03 00 00 00 01 00 08 00 00 01 03 00 03 00 00 00 01 00 01 00 00 01 06 00 03 00 00 00 01 00 01 00 00 01 11 00 04 00 00 00 01 00 00 03 e8 01 15 00 03 00 00 00 01 00 01 00 00 01 16 00 04 00 00 ... 58500 more bytes>,
  byteLength: 58600
}
```



using ipfs 

decode / deserialize

