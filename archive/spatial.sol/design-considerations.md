---
description: Work in progress - comments very welcome! @astralprotocol
---

# Design Considerations

Any comments or feedback please reach out [@astralprotocol](https://twitter.com/astralprotocol) on twitter or via [Discord](https://discord.gg/q76DWRhPdh).

## Representing geographic vector features

How to represent these features on chain: `struct`, `array` or otherwise? We want to balance efficiency, simplicity and developer experience.

Our initial impulse is to mirror GeoJSON as it is the de facto standard for web developers, well documented and a familiar concept. So a `struct` is a sensible approach, with `s.coordinates` being the coordinate array `[[lon0, lat0], [lon1, lat1], [lon2, lat2], ... ]`:

```text
enum FeatureType { Point, LineString, Polygon } // MultiPoint? MultiLineString? MultiPolygon?

struct Point {
    FeatureType type, // set to FeatureType.Point
    int[2] coordinates // [lon, lat]
}

struct LineString {
    FeatureType type, // set to FeatureType.LineString
    int[][2] coordinates // [[lon0, lat0],[lon1, lat1], ... ,[lonN, latN]]
}


struct Polygon {
    FeatureType type, // set to FeatureType.Polygon
    int[][][2] coordinates // [[lon0, lat0],[lon1, lat1], ... ,[lonN, latN]]
}

// not sure if my nested array syntax is right lol
```

Then we would call `length(s)`, which would compute the length of the linestring represented by `s.coordinates.`This also would enable efficient type checking and verification when data is onboarded or used in a method:

```text
LineString s = LineString(FeatureType.LineString, [[0,0],[1,1],[1,2]])

function length (Feature inputFeature) public returns (int length) {
    require(inputFeature.type == "LineString", "can only calculate the length of a linestring");
    // Calculate the length
    return length;
}
// lol forgive my horrendous pseudocode
```

## Coordinate Reference Systems

How do we want to handle different coordinate reference systems? Do we want to plan on supporting various systems? We think it is probably an aspirational goal, but realistically a requirement that we don't think we need to worry about too much for a long time.

For now we think we want to just focus on mirroring the standards adopted by GeoJSON, especially for v0. \(Interesting that GeoJSON [removed support](https://www.avenza.com/resources/blog/2017/01/31/handling-geojson-files-unspecified-projected-coordinate-systems/) for alternative coordinate reference systems in 2016 "because of interoperability issues".\)

> The coordinate reference system for all GeoJSON coordinates is a geographic coordinate reference system, using the World Geodetic System 1984 \(WGS 84\) \[WGS84\] datum, with longitude and latitude units of decimal degrees. This is equivalent to the coordinate reference system identified by the Open Geospatial Consortium \(OGC\) URN urn:ogc:def:crs:OGC::CRS84. 
>
> An OPTIONAL third-position element SHALL be the height in meters above or below the WGS 84 reference ellipsoid. In the absence of elevation values, applications sensitive to height or depth SHOULD interpret positions as being at local ground or sea level.
>
> [https://datatracker.ietf.org/doc/html/rfc7946\#section-4](https://datatracker.ietf.org/doc/html/rfc7946#section-4)

This decision would be based on a few observations:

*  We want these contracts to be composable - dapps will be built that permissionlessly call other spatial data registries deployed on a blockchain. Even if we had a contract- or feature-level `CRS` flag, handling a range of coordinate reference systems would cause complexity to balloon
* Early on especially we don't anticipate precision location based applications to be running on any smart contract platforms. This is partly because positioning systems are neither hyper precise nor trustless. This disclaimer should be included in the code - that precision may vary. It will be a long time before these technologies mature to the point that they can support mission critical location-based applications - for now our bias towards action and the pragmatic, progress-oriented critical path leads us to lean towards just adopting the most commonly used coordinate reference system used on the web. 
* WGS84 supports a third element in the coordinate array: altitude. This is powerful because it means Spatial.sol / other Astral standards would be built to support working with 3-dimensional volumes from the outset. That said, this adds significant complexity and would likely 

## Consistency

* We need to establish a consistent way of working with these features. i.e. Always passing around the entire struct and not sometimes passing `s.coordinates` into a function.

## Features as contract instances?

* Is there any benefit to taking the [Platin approach](https://github.com/platinprotocol/solidityGEO) and having these geographic features be contract instances in their own right? Then we could have methods - `s.length()` returns the length of the linestring - but it seems super inefficient and probably unnecessary.

## eth-spatial client libraries

Solidity has certain quirks that makes it tricky to work with. Our focus is on developer experience - we want to make it as easy as possible for dapp developers to build spatial and location-based decentralized applications. 

So we expect we will need to develop client libraries that effectively serve as a transpiler. We're not exactly certain how this will work, but a few ideas:

* These client libraries - imagine `eth-spatial.js` and `eth-spatial.py` to start - are designed to provide a developer friendly interface between vector spatial data represented in JavaScript / Python environments and those represented in the EVM.
* This could mean moving from JS / Python -&gt; EVM and preparing GeoJSON for submission to a contract that uses Spatial.sol. This would happen by, for example, converting decimal degrees coordinates to Solidity-friendly integers.
* A well-designed client transpiler library would also improve the efficiency of the system by performing checks to make sure that no errors will arise off chain, and helping devs be confident that data they're submitting in an Ethereum transaction are valid and won't be rejected by the contract.
* These client libraries should be designed to interoperate with `web3.js` or `ethers.js`, extending those when the developer is interacting with contracts that use Spatial.sol.

```text
const Web3 = require('web3')
const ethSpatial = require('eth-spatial')

let web3 = new Web3(...);
let web3spatial = new ethSpatial(web3);
```

\(or something like that - to give the instance of `web3` access to all of the required methods etc to work with spatial contracts\)

