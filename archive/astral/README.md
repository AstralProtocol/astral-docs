# A Web3-Native Geospatial Vision

### Context: Cloud-Native Geospatial

Satellite images are big. One 8-band Landsat 7 scene we examined (`LE71660522010289ASN00`) is nearly 850MB. These datasets are rich with information about the state of the Earth's surface at the moment of capture, immensely valuable snapshots of the state of our world that can be studied for decades - centuries to come. However, traditional client-server data architectures make it infeasible for non-specialists to work with these large raster datasets. Download times slow workflows, and consumer-grade hardware is incapable of visualizing and analyzing these datasets.

{% tabs %}
{% tab title="Cloud-Optimized GeoTIFFs (COGs)" %}
To solve this problem, the satellite imagery community has designed the [Cloud-Optimized GeoTIFF](https://www.cogeo.org/) (COG) standard. COGs are GeoTIFFs, but they are organized so that they can be hosted in the cloud and users can send HTTP range requests to only access the parts of the file they need, when they need them. By tiling the image, users only need to request the geographic extent relevant to their workflow; overviews allow users to load lower resolution versions of the image, which is often all that is required in many applications. COGs are a major step forward to unlock the potential of earth observation data, and a key component of the cloud-native geospatial vision the community is moving toward.&#x20;

(Next read about STAC catalogues ->)
{% endtab %}

{% tab title="SpatioTemporal Asset Catalogs (STAC)" %}
The Cloud-Native Geospatial community has designed another specification, intended to complement COGs: [SpatioTemporal Asset Catalogs](https://stacspec.org/). "The SpatioTemporal Asset Catalog (STAC) specification provides a common language to describe a range of geospatial information, so it can more easily be indexed and discovered." ([https://stacspec.org/](https://stacspec.org/)).

The problem was that various satellite imagery providers were using their own custom-designed systems for indexing and cataloging satellite images and other spatio-temporal assets. Each of these indexing systems were roughly the same, but were not interoperable. STAC standardizes the way these collections of data are organized and referenced.

STAC Items are single spatio-temporal data assets - for example, a single Landsat scene with associated metadata. STAC Catalogs are JSON files that includes links to Items and sub-Catalogs. This can be thought of as a directory structure, with Catalogs acting as folders and Items acting as files - Catalogs can contain Catalogs (sub-folders) or Items. This simple, flexible system allows users to organize large volumes of satellite imagery and - crucially - quickly and easily search through the assets available.
{% endtab %}
{% endtabs %}

![](https://static.eos.com/wp-content/uploads/2020/09/landsat\_7\_sample\_img\_01.jpg)

_From_ [https://eos.com/landsat-7/](https://eos.com/landsat-7/)

### Web3-Native Geospatial

Cloud-native geospatial technologies are key to scaling the geospatial data sector, and for the efficient discovery and computation of relevant data. However, they are built in a centralized computing paradigm, with roots still in the client-server model. Data networks designed in this way are brittle - links can break, file content can be changed unbeknownst to users, and data must be held by trusted custodians who may abuse their role as maintainers of server systems holding geospatial data.

A more secure, resilient and user-centric vision for the Internet is evolving with Web3. Decentralized identifiers, peer-to-peer storage and transfer, and content identifiers resolve the most critical fragilities that exist in the incumbent web.

The geospatial data sector is not immune to these problems - in fact, the ecosystem is rife with inefficiencies. Many organizations hold multiple versions of the same reference spatial datasets on various internally-operated servers. Each of these servers requires computing resources and skilled workers to maintain. It seems unlikely that each of these datasets is kept up to date based on update release cycles, meaning the reference data upon which the organizational data is overlaid is not current. Deep architectural wastefulness pervades geospatial data storage systems in the public, private and third sectors worldwide.

The Web3-native geospatial vision seeks to integrate the learnings of the incumbent geospatial data practitioners with the principles underpinning the design of the decentralized web.

* **Data must persist** — we cannot try to resolve a mission-critical dataset a few years after its creation only to receive a 404 error. This is especially true for spatial finance applications where decisions dealing with large monetary values are made based on insights derived from geospatial data.
* **Datasets must be verifiable** — all parties can have cryptographic confidence when accessing a dataset around the world and into the future that they are looking at the same information as others.
* **Data networks must be resilient** — they must be self-healing and resilient to the failure of any actor.
* The **right to privacy** must be built in on the technical layer, not added on top of system design at the policy layer.

These are challenging problems to solve, and the community is early in the process of developing the standards, tools and protocols that will unlock the potential of the decentralized, location-based web.

In this talk, the core team from the Astral Protocol will outline their vision for a Web3-native geospatial data architecture, including data storage and computation systems that are decentralized and fault tolerant, and in which all participants are cryptoeconomically-aligned. The Astral team will touch on data storage systems they are designing based on IPFS, Filecoin, Arweave and Ceramic, and will share insights into decentralized geospatial data processing and discovery systems including dClimate, Ocean Protocol and Algovera AI. They will also touch on their early research into privacy-preserving geospatial technologies.

These technologies are designed to interoperate with distributed ledgers, smart contracts and digital currencies, with an eye towards underpinning the emerging regenerative finance ecosystem being built on public blockchains.



####
