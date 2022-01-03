# A Web3-Native Geospatial Vision

## Web3-Native Geospatial

### Cloud-Native Geospatial

Satellite images are big. One 8-band Landsat 7 scene we examined \(`LE71660522010289ASN00`\) is nearly 850MB. These datasets are rich with information about the state of the Earth's surface at the moment of capture, immensely valuable snapshots of the state of our world that can be studied for decades - centuries to come. However, traditional client-server data architectures make it infeasible for non-specialists to work with these large raster datasets. Download times slow workflows, and consumer-grade hardware is incapable of visualizing and analyzing these datasets.

![](https://static.eos.com/wp-content/uploads/2020/09/landsat_7_sample_img_01.jpg) 

_From_ [https://eos.com/landsat-7/](https://eos.com/landsat-7/)

**Cloud-Optimized GeoTIFFs**

To solve this problem, the satellite imagery community has designed the [Cloud-Optimized GeoTIFF](https://www.cogeo.org/) \(COG\) standard. COGs are GeoTIFFs, but they are organized so that they can be hosted in the cloud and users can send HTTP range requests to only access the parts of the file they need, when they need them. By tiling the image, users only need to request the geographic extent relevant to their workflow; overviews allow users to load lower resolution versions of the image, which is often all that is required in many applications. COGs are a major step forward to unlock the potential of earth observation data, and a key component of the cloud-native geospatial vision the community is moving toward.

#### SpatioTemporal Asset Catalogs

The Cloud-Native Geospatial community has designed another specification, intended to complement COGs: [SpatioTemporal Asset Catalogs](https://stacspec.org/). "The SpatioTemporal Asset Catalog \(STAC\) specification provides a common language to describe a range of geospatial information, so it can more easily be indexed and discovered." \([https://stacspec.org/](https://stacspec.org/)\).

The problem was that various satellite imagery providers were using their own custom-designed systems for indexing and cataloging satellite images and other spatio-temporal assets. Each of these indexing systems were roughly the same, but were not interoperable. STAC standardizes the way these collections of data are organized and referenced.

STAC Items are single spatio-temporal data assets - for example, a single Landsat scene with associated metadata. STAC Catalogs are JSON files that includes links to Items and sub-Catalogs. This can be thought of as a directory structure, with Catalogs acting as folders and Items acting as files - Catalogs can contain Catalogs \(sub-folders\) or Items. This simple, flexible system allows users to organize large volumes of satellite imagery and - crucially - quickly and easily search through the assets available.

### Web3-Native Geospatial

Cloud-Native Geospatial technologies are key to scaling the geospatial data sector, and for the efficient discovery of relevant data. However, they are built in a centralized computing paradigm, with roots still in the client-server model. Data networks designed in this way are brittle - links can break, files can be changed unbeknownst to users, and data must be held by trusted custodians who may abuse their role as maintainers of server systems holding geospatial data.

While these issues can be tolerated or designed around, a more secure and robust vision for the Internet is evolving with Web3. Decentralized identifiers, peer-to-peer storage and transfer, and content identifiers resolve the most critical fragilities that exist in the incumbent web.

The geospatial data sector is not immune to these problems - in fact, the ecosystem is rife with inefficiencies. Many organizations hold multiple versions of the same reference spatial datasets on various internally-operated servers. Each of these servers requires computing resources and skilled workers to maintain. It seems unlikely that each of these datasets is kept up to date based on update release cycles, meaning the reference data upon which the organizational data is overlaid is not current. Deep architectural wastefulness pervades geospatial data storage systems in the public, private and third sectors worldwide.

The Web3-Native Geospatial vision seeks to integrate the learnings of the incumbent geospatial data practitioners with the principles underpinning the design of the decentralized web.

* **Data must persist** - we cannot try to resolve a mission-critical dataset a few years after its creation only to receive a 404 error. 
* **Datasets must be verifiable**, so that all parties can have cryptographic confidence when accessing a dataset around the world and into the future that they are looking at the same information as others. 
* **Data networks must be antifragile**, resilient to the failure of any actor. 
* **The right to privacy must be built in**, not layered on top of system design.

These are challenging problems to solve, and the community is early in the process of developing the standards, tools and protocols that will unlock the potential of the decentralized, location-based web.

#### GeoDIDs

[Geographic decentralized identifiers](https://docs.astral.global/geodids/geodid-core-specification), or GeoDIDs, are DIDs designed to identify spatial data assets and to be compatible with any distributed ledger or network. In creating a GeoDID, data controllers permissionlessly create irrevocable, cryptographically-verifiable identities for spatial data assets that can be useful in decentralized applications - a Web3-native way to identify spatial data.

The work on geographic decentralized identifiers is being progressed by the team at [Astral](https://astral.global/), supported by a development grant from the [Filecoin Foundation](https://filecoin.io/). The team recently released an alpha version of a GeoDID Method Specification, which defines an approach in creating, reading, updating and deleting identifiers for these assets using DIDs. However, through this work the team has learned that it may not be appropriate to use its own DID Method Specification for identifying these data assets, but to instead publish a metaspecification: a standard data format that any DID could incorporate. This would mean that any decentralized identifier could identify a spatial data asset, unlocking a large amount of flexibility in how GeoDID technology could be developed.

A GeoDID effectively wraps a reference to an existing spatial data asset in a DID Document. The endpoint or content identifier \(CID\) where the spatial data asset can be retrieved from is included in the DID Document's `service` array. The core specification is intentionally very lightweight, designed to support legacy and future spatial data formats. These data formats will be supported by a list of GeoDID Extensions, which standardize how GeoDIDs identifying assets of that format are structured - meaning code can be written to work with those standard formats by uncoordinated developers or, more likely, software packages can be written to work with data compliant with the standard. GeoDIDs can be public or peerwise.

**A Rationale for GeoDIDs**

The GeoDID is intended to imbue identifiers for spatial data assets with the standards that Web3 applications demand. "Don't trust - verify". To enable location-based decentralized applications and smart contracts that are trustless and immutable for self-sovereign users, the data used in the system must be reliably there.

This might sound like an overengineered solution. Why store a reference to a spatial dataset on a blockchain? Why store the spatial dataset itself on a decentralized, permanent substrate like Arweave? Aren't HTTPS URLs and Amazon S3 buckets much easier?

We anticipate that in the coming century, spatial / sensor data technologies will come to underpin significant portions of the world economy. The emerging field of [spatial finance](https://www.smithschool.ox.ac.uk/research/sustainable-finance/research-sf.html) - "the application of geospatial data technologies to financial theory and financial practice" \(Caldecott\) - shows great promise to undermine a timeless problem and realign financial incentives with our moral imperative to preserve the health of our Earth. If spatial finance continues to grow and traditional finance is consumed by decentralized finance - and we expect that it will be to a great extent, given the profound efficiency improvements DeFi enables - then a wide range of spatial DeFi applications will emerge in the ecosystem. Imagine a £100M sovereign bond linked to sustainability metrics derived from satellite imagery: the importance of Web3-native geospatial technologies for trustworthy verification of the bond become clearer.

Furthermore, GeoDIDs are intended to be useful in smart contracts. Blockchains are expensive places to store data - it is unlikely that most spatial datasets will be stored on-chain in full. However, if a GeoDID is written to a smart contract, the contract has an immutable reference, a persistent identifier to a spatial data asset that is controlled by the registrant. This technology is nascent, and its designers do not comprehend what its implications may be - but the opportunity space is vast.

**GeoDIDs under the hood**

The GeoDID is inspired by the SpatioTemporal Asset Catalog \(STAC\) specification and utilizes a similar linked data structure. The structure alleviates a handful of problems associated with traversing large datasets, and allows for ease of use for the end user. Spatial data assets are identified in the service endpoints of the GeoDID document. These service endpoints can be classed as either Collections or Items. Each "Collection" contains a number of child Collections or Items; and each "Item" will contain several service endpoints that resolve to geospatial data assets. This hierarchy of encapsulating linked data within the GeoDIDs will allow for user's to find or create the data/datasets that they need easily.

The alpha implementation of the GeoDID specification is under development at [https://github.com/AstralProtocol/astralprotocol](https://github.com/AstralProtocol/astralprotocol). For the initial version, only public GeoDIDs are supported. A mapping of GeoDID =&gt; GeoDID Document URLs is stored in a smart contract, granting DID Controllers sovereignty over their DIDs and ensuring that permissionless, permanent resolution is possible. Testing is ongoing on Ethereum's Ropsten testnet, but the team expects to deploy the first version of production GeoDID contracts to an Ethereum sidechain, likely Polygon \(formerly Matic\). This will ensure that the cost of registering a GeoDID is low.

It is important to note: GeoDIDs are blockchain agnostic. A blockchain is not required. This is an intentional design decision, intended to accommodate users who, for whatever reason, may not be able to rely on public blockchains in their data architectures. We believe that public blockchains offer significant advantages that should not be overlooked - but we also recognize that organizations must operate within technical and regulatory constraints that may require them to avoid their usage until the technology is more mature. GeoDIDs and GeoDID Documents can be easily configured to resolve on private distributed ledger instances or centralized databases. It should be stressed that this might undermine some important qualities of the DID. See Decentralized Identifiers for further explanation.

#### Future Work

Plans to develop an IPLD encoding for vector datasets are being developed, but many technical challenges are foreseen. Content identifiers present interest opportunities for identifying geographic extents - hierarchical topologies naturally adhere to a parent-child-like tree structure. A national border could be represented as a CID; child nodes would identify subsidiary jurisdictions like states or regions, counties, cities, land parcels, and individual buildings. Early ideas around developing capabilities to compare the topologies of CID-encoded vector geometries are being discussed by the team.

![](https://i.imgur.com/7tw907x.png)

_Wales, Welsh Electoral Divisions and Welsh Parish Regions, from_ [_Ordnance Survey's Boundary-Line dataset_](https://osdatahub.os.uk/downloads/open/BoundaryLine)_._

Additionally, the next phase of research and development will be for GeoDIDs that support spatial querying and clipping. DIDs support selectors, paths, query parameters and fragments. These additional details that can be included in a GeoDID offer a powerful way to efficiently represent and store large spatial datasets in a much more resource-constrained manner that is still persistent, cryptographically verifiable and optionally private.

For example, consider GeoDID representing a collection of satellite imagery. We should be able to specify a a spatial and temporal subquery in the GeoDID itself. That way, a user could store a single GeoDID that specifies a single image, clipped to a particular area, extracted from the GeoDID Collection. The user would not need to store that clipped image, but only the GeoDID with query parameters - they would still have the confidence that the GeoDID would resolve to the same clipped image permanently. The same principles apply to vector datasets. A Web Feature Service request contains selection parameters in the URL query string's xml filter, and resolves to a user-defined subset of the dataset served by the WFS. A GeoDID containing a query would likewise resolve to such a subset, but with the persistence, user control and cryptographic verifiability DIDs afford.

This functionality seems to be crucial for an efficient geospatial Web3. One use case: auditing spatial finance applications. A satellite image might prove that a particular green infrastructure project was completed by a certain date, or that some insured natural capital warranted a payout. A GeoDID selecting a vector polygon - the project site - could be stored on chain, as could a series of GeoDIDs representing a sequence of satellite images clipped to that area, before, during and after construction. Investors could audit their green bonds with such a system, confident that audit records will be available for decades to come.

The Web3-native geospatial web is nascent, but ripe with potential to serve as a core component of a more resilient Internet. Much work within the Web3 ecosystem is focusing on how programmable money can be applied to solve intractable problems that have always plagued humanity. Integrating geospatial insights into this mechanism design could be a limited - but potent - tool in the toolkit.

