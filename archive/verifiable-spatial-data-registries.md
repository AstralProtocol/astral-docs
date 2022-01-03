---
description: Smart contracts for raster and vector spatial data assets
---

# Verifiable Spatial Data Registries

Leveraging [Spatial.sol](spatial.sol/), we are early in the process of developing a standard contract for **verifiable spatial data registries**. There is a wide breadth of opportunities in this design space.

Specifically, we are building on work we've done to let self sovereign users register geographic zones on smart contract platforms, starting with EVM-compatible chains. This capability is required for a number of use cases - a spatial governance system like [Hyperaware](https://hyperaware.io), sustainability-linked bonds and other spatial DeFi applications, parametric insurance policies like those [IBISA](https://ibisa.network) provides, location-based Web3 games including AR and [Pebble Go](https://twitter.com/pebble\_go), and so on.

We believe that a smart contract standard would promote the composability of these spatial data registries. We see value in building on existing work and designing these spatial data registries to interoperate with existing protocols. To this end, our plan is to represent these spatial data assets - vector or raster data objects - as tokens.&#x20;

We will likely extend the ERC721 contract standard and represent geographic zones as NFTs, meaning they can interoperate with ERC721-compatible dapps, be owned and transferred, etc. We'll extend the contract, though, to include geospatial operations - for example, we plan to include a method that checks if a point supplied is contained within the boundaries of a specific zone: `` zoneContains(zoneID, coordinates) returns (bool)` ``.&#x20;

Before making this decision, however, we want to look into ERC998 and the potential of a composable spatial data registry. The hierarchical ownership model of ERC998 maps very nicely to the hierarchical nature of administrative boundaries - nations are composed of states or provinces, which are composed of counties etc. Research to be done.

### Justification

Land registry contracts exist, for both virtual and real-world land parcels - [Decentraland](https://decentraland.org), [Etherland](https://etherland.world/marketplace/), [Superworld](https://www.superworldapp.com), [Geo Web](https://www.geoweb.network), [Cryptovoxels](https://www.cryptovoxels.com) and others. However, these almost always restrict users to owning grid cells, due to the complexity of representing irregular polygons in a smart contract. A land registry where two users could own the same piece of land would not be realistic - detecting these topological intersections is difficult.

It is our belief that for spatial data registries to be useful in real world contexts, they must support irregular polygons. This means that we need to be able to detect zone intersections, which could result in a piece of land being double-insured, or a vehicle being in two congestion zones at once. This was the inspiration for our initial experiments writing `Spatial.sol`.

### Vision

The spatial data registries standard we are designing aims to achieve the representation of this _physical scarcity_ applied to physical territory within a spatial reference system. These are "non-intersecting" boundaries, defined as Type 1 jurisdictions by [Hooghe and Marks (2003)](https://www.researchgate.net/publication/248233581\_Unraveling\_the\_Central\_State\_but\_How\_Types\_of\_Multilevel\_Governance).

We intend to achieve this by performing zone intersection checks using `Spatial.sol,` which will have functions that allow us to check if zones intersect. Our goal is to create a verifiable, trustless way of detecting these boundary disputes, if necessary. This will likely require some kind of on-chain spatial indexing system, helping us minimize the number of `intersects` calls to make by only testing polygons known to be in the vicinity of a newly-registered polygon.

We're researching how to efficiently design a system that would enable this kind of a spatial data registry, along with requirements. We're trying to work out exactly what the needs might be and anticipate that this will emerge as a contract standard. We can imagine many variations of this type of contract deployed, each storing its own registry of polygons - for mobility apps, administrative jurisdictions, maritime governance zones, restricted airspace, watersheds and so on. The initial design will be tailored to registering geographic zones (i.e. polygons). Use cases will likely emerge that require the registration of other spatial data assets like points and lines, or raster datasets such as satellite images and LIDAR scans; we will consider these, but focus on our core use case of a zone registry.

### An Early Use Case

One early adopter of the verifiable spatial data registry standard is the Kolektivo Framework, which is designing a Decentralized Exchange Trading System that relies on natural capital currencies. The Kolektivo implementation of these currencies, which are backed by ecosystem assets and ecosystem services, will rely on Astral's verifiable spatial data registries.&#x20;

Another early adopter is Geo Web, "a set of open protocols with a system of property rights for anchoring digital content to physical land" ([Geo Web Gitcoin grant](https://gitcoin.co/grants/1403/the-geo-web)). At the moment Geo Web parcels are grid cells, a regular raster. By using Astral verifiable spatial data registries, version 2 of the Geo Web protocol could support irregular geometries as NFTs - an application much better suited to mirror the real, physical world.

Ultimately we aim to publish an Ethereum Improvement Proposal describing this new standard and develop an open source reference implementation in Solidity.

### Questions

* Who has the right to create or register parcels / zones? Under what conditions?&#x20;
* Can zones overlap / intersect?&#x20;
* How can we build tools to gracefully recover from lost or abandoned parcels?


