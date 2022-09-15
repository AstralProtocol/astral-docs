---
description: Geospatial Non-fungible Token
---

# GeoNFT

A GeoNFT represents geospatial assets by extending the non-fungible token (ERC-721) contract with location information.

Geospatial data is defined as a GeoJSON string defining a `FeatureCollection` of one or more `Features` (`Polygon` or `Point`):

```typescript
export const GEOJSON2: FeatureCollection<Polygon> = {
  type: "FeatureCollection",
  features: [
    {
      type: "Feature",
      properties: {
        area_m2: 417.54,
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [-68.8906744122505, 12.147418397582491],
            [-68.8907468318939, 12.147347599447487],
            [-68.8907213509083, 12.14723615790054],
            [-68.8905939459801, 12.147198136656193],
            [-68.89051884412766, 12.147280734524921],
            [-68.89055103063583, 12.147379065287602],
            [-68.8906744122505, 12.147418397582491],
          ],
        ],
      },
    },
  ],
};ty
```

Additionally, GeoNFTs contain an `Ecological Index` as a measure of ecological state:

```solidity
struct EcologicalIndex {
        string indexType;
        int256 indexValue;
}
```

The `Ecological Index` is an on-chain variable representing the value of the asset defined by the GeoNFT. A common design pattern is to fractionalize an NFT into fungible ERC-20 tokens for usage within community reserves and currencies. The `Ecological Index` could be a parameter to determine the amount of ERC-20 tokens that are created. As the `Ecological Index` changes, the supply of tokens may be responsive to this value.

