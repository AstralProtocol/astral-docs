# GeoDID Extensions Overview

Each spatial data asset is referenced in an object stored in the GeoDID document's array of service endpoints. This allows a single GeoDID to represent multiple spatial data assets, including of heterogeneous types \(shapefiles with GeoTIFFs, multiple LIDAR point clouds, etc etc.\)

One of the required attributes contained in the `service` objects is the format of the spatial data asset referenced: `geotiff`, `shapefile`, `geojson` \(?\) etc. For v0.0, we have implemented `geotiff`, `geojson` and `stac-json` and `stac-ipld` spatial data asset types. These attributes allow the `@astral-protocol/astral-_______` \(@Jared?\) module to resolve and unpack the spatial data asset appropriately.

// Compression? `shapefile-zip`, or `{"type": "geojson", "compression": "gzip", ... }`

Table: GeoDID Extensions

