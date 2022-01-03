# GeoDIDs

When sensor measurements are captured digitally, the information is formatted to be processed by some software. Spatial data comes in many different formats - GeoJSON, KML, shapefiles, GeoTIFFs, cryptospatial coordinates etc etc.

Astral endeavors to design an open and agnostic protocol that will gracefully develop and evolve with the state of spatial computing. We also expect full trustlessness, self sovereignty and independent verifiability of all protocols we design. This requires a versatile, Web3-native spatial data identification, encoding and storage scheme.

To achieve this, with support from the Filecoin Foundation and London Blockchain Labs, we have drafted a [GeoDID Method Specification](https://docs.astral.global/geodids/geodid-core-specification) and [prototype modules and smart contracts](https://github.com/AstralProtocol/astralprotocol) to create, read, update and deactivate these geographic decentralized identifiers and the data assets they reference.

GeoDIDs will identify these files by wrapping the spatial data assets in DID documents, thereby providing a standard schema to grant the user verifiable control and enable trustless interoperability. Different spatial data formats will be supported through GeoDID Extensions - meaning GeoDIDs can support any current or future digital spatial data format. Required member variables will include relevant metadata to enable comprehensive indexing and use of the spatial data a GeoDID identifies.

We have designed the initial draft of the spec and would be curious for feedback from you or anyone interested when we release the spec to the community for review. 

GeoDIDs are agnostic to the spatial data assets being identified. However, we are designing the alpha implementation of the GeoDID modules to rely on IPFS by default, so we can cryptographically verify the integrity of the data assets referenced.

The GeoDID Method Specification can be found [here](../geodids/geodid-core-specification/), and writing on the extensions [here](../geodids/geodid-extensions-1/). A repository containing our prototype implementation of a GeoDID system is [here](https://github.com/AstralProtocol/astralprotocol).

