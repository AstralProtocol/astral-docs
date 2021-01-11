# GeoDID Specification

The GeoDID specification will act as the default Web3 specification for working with geo-spatial data sets. Each DID Document will contain several assets endpoints and its respective metadata. The IPLD encoded GeoTIFFs will be implemented through an IPLD codec that will encode the GeoTIFF and enable GET Range requests, by a byte serving technique that will query the proper bytes through IPLD selectors.

