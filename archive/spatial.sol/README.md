---
description: A Solidity library of topological and geometric functions
---

# Spatial.sol

Many of the applications we envision will require us to perform spatial operations in smart contracts. To this end, a few years ago (at ETHParis) we outlined and experimented with a Solidity library for performing these operations - measuring the length of a linestring, testing to see if lines intersect, checking to see if a point is inside a polygon, etc. Our draft code is [here](https://github.com/AstralProtocol/spatial-sol/blob/master/contracts/Spatial.sol).

We prototyped a location-aware wallet (early experiments that may lead to truly [**local** currencies](https://ethresear.ch/t/how-to-implement-digital-community-currencies-with-ethereum/8801)). At the time we were discouraged due to computational complexity leading to high gas costs, but Layer 2 solutions like Polygon and xDai, alternative lower cost EVM-compatible blockchains like IoTeX or Avalanche and, of course, Eth2 does mean that these kinds of operations will be increasingly viable in smart contracts.

We are developing the first version of the `Spatial.sol` library and plan to release it under an open source license. Developing the library entails tackling several technical challenges, and to build a production-quality library will be quite involved.

### Spatial.sol

`Spatial.sol` is required for many of the location-based dapps and spatial contracts we envision, including the verifiable spatial data registries described [here](../verifiable-spatial-data-registries.md). We are researching which functions the library should include, and will look to [Turf.js](https://turfjs.org) for inspiration. Some functions we expect to include are:

* Boolean verification algorithms like `isPolygon`, `isLine` and so on
* `sqrt`
* Conversion helper functions like `degreesToNanoradians.`
* Various geometric functions like `distance`, `area`, `centroid`, `length`, `perimeter`
* Angular functions like `bearing`, `rhumbBearing`
* Geometric helper functions like `boundingBox, convexHull`
* Boolean topological tests like `pointInBbox`, `pointInPolygon`, `intersects`
* Functions for manipulating geometries such as `difference`, `dissolve`, `intersect`, `union`, etc.

These functions will serve as a basis for the first cohort of applications built on Astral. Note that these are primarily **vector** operations - we anticipate that raster analysis techniques may be useful (recreating some of the functionality of [RasterIO](https://rasterio.readthedocs.io/en/latest/), for example), but will leave that for a future version of Spatial.sol. We still need to research the feasibility of supporting multifeature data structures like multipoints, multilines and multipolygons, as well as more complex shapes like polygons with holes. Version 1 will not support 3-dimensional volumes (polyhedra), but we anticipate that many use cases will require implementation of this functionality in future - for example, to test if an aircraft has entered some airspace.&#x20;

#### Spatial Reference Systems

We anticipate that one of the most difficult aspects of building  smart contracts designed to work with spatial data is accommodating the diversity of [spatial reference systems](https://en.wikipedia.org/wiki/Spatial\_reference\_system). The Earth is not a perfect sphere - it is a geoid - and many different systems are used to represent positions relative to the planet. [Geodesy](https://en.wikipedia.org/wiki/Geodesy) matters, and implementing systems that accommodate different spatial reference systems, converting between them etc will be a complex technical challenge.&#x20;

For v1 of Spatial.sol we will minimize accuracy and complexity in favor of developing simplified on-chain geospatial computing capabilities. For example, we will likely implement a [Haversine](https://en.wikipedia.org/wiki/Haversine\_formula) function, but not a [Vincenty](http://www.movable-type.co.uk/scripts/latlong-vincenty.html) function.

### Trigonometry.sol

`Spatial.sol` has a dependency: `Trigonometry.sol`, developed and open sourced by Sikorka ([docs](https://github.com/Sikorkaio/sikorka#trigonometry), [code](https://github.com/Sikorkaio/sikorka/blob/master/contracts/trigonometry.sol)). This library appears to have been abandoned a few years ago, and lacks a `tangent` method, which is useful in some operations like the [bearing](https://github.com/Turfjs/turf/blob/41a123a0e151be6a7e312dfecb91b69c4ff3f3f2/packages/turf-bearing/index.ts#L53) between two points. `Spatial.sol` will require an audited `Trigonometry.sol` to be secure.

### eth-spatial.js

&#x20;We anticipate that we'll want to develop a corresponding client library `eth-spatial.js`, to abstract some of the complexities of supplying spatial data to contracts using Spatial.sol. Our goal is to ease the developer experience - we expect that many developers will be working with GeoJSON in the client.&#x20;

`eth-spatial.js` will be designed to seamlessly accept common data formats used on the web (starting with GeoJSON) and prepare the spatial data for use in contracts that use the `Spatial.sol` library. One example process here will be converting decimal degrees to integers to be used in the contract, possibly nanoradians.&#x20;

Likewise, our aim is for `eth-spatial.js` to easily convert from on-chain spatial data to web-ready GeoJSON. We may look into developing a subgraph to index on-chain geospatial data - the final step to fetching this data will be presenting it in a format that interoperates with common spatial data libraries like Leaflet, Mapbox GL JS etc. An `eth-spatial.py` library would also probably be helpful, as would implementations in other languages - future work to do.

### Future

We anticipate this library will need a thorough audit. We would like to explore how we can ensure ongoing support and development of the library once it is developed and open sourced.
