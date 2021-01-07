---
description: A primer on geographic decentralized identifiers
---

# Intro

A GeoDID is a [decentralized identifier](https://w3c-ccg.github.io/did-spec/) for identifying _**spatial data assets**_ for use in Web3 applications.

GeoDIDs are:

> **✅ User-controlled.**  
> DIDs are independently created in a permissionless way: no centralized authority is required to approve or issue identifiers.
>
> **✅ Cryptographically-verifiable.**  
> DIDs are controlled using cryptographic keys. \(more detail here?\)
>
> **✅ Versatile and platform agnostic.**  
> GeoDIDs are designed to represent spatial data assets in as flexible a way as possible. This means they can be adapted to suit user requirements - important for enterprise and government adoption.
>
> **✅ Web3-native. \(?\)**  
> GeoDIDs are optimized to be decentralized. \(more detail and justification here\)

\[sweet satellite image here\]

###

### GeoDIDs

#### The Core Specification

> We are early in developing the GeoDID spec. For now, we are focused on storing `geojson` vector spatial data structures, and `geotiff` raster data. The GeoDID specification is designed to be flexible and identify any spatial dataset in any format - even ones that haven't been developed yet.

#### GeoDID Extensions

Each spatial data asset is referenced in an object stored in the GeoDID document's array of service endpoints. This allows a single GeoDID to represent multiple spatial data assets, including of heterogeneous types \(shapefiles with GeoTIFFs, multiple LIDAR point clouds, etc etc.\)

One of the required attributes contained in the `service` objects is the format of the spatial data asset referenced: `geotiff`, `shapefile`, `geojson` \(?\) etc. For v0.0, we have implemented `geotiff`, `geojson` and `stac-json` and `stac-ipld` spatial data asset types. These attributes allow the `@astral-protocol/astral-_______` \(@Jared?\) module to resolve and unpack the spatial data asset appropriately.

// Compression? `shapefile-zip`, or `{"type": "geojson", "compression": "gzip", ... }`

Table: GeoDID Extensions

### Storing spatial data

Web3-native storage: IPFS

CID, URI, whatever.

### Creating GeoDIDs

### Reading / Resolving GeoDIDs

### Updating GeoDIDs

### Deleting GeoDIDs

Public GeoDIDs: if registered on a public blockchain, \_\_\_\_.

###
