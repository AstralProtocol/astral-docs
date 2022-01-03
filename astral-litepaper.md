# Astral Litepaper

## Astral <a href="#astral" id="astral"></a>

For the past few years we’ve been investigating what we see as a new galaxy in the Web3 universe, at the intersection of spatial data and consensus technologies. We’ve explored the boundaries of the design space researching, prototyping and building community. This is culminating in our work to build what we now see as the key primitives to underpin a new category of Web3 applications using spatial and location data. Our work at Astral is focused on promoting the evolution of an open, human-centered and composable location-based decentralized web.

The opportunity space is pretty vast. We believe that the vision for the user-controlled internet is incomplete without peer-to-peer alternatives to services like Uber, Google Maps, Airbnb, Tinder, Craigslist, Amazon and others. Even more exciting is the opportunity to replicate the functionality required for systems of local taxation, voting, and physical security. Perhaps the most exciting of all is the notion that our systems of value exchange can be configured to promote the preservation of life and ecological health — the nascent “regenerative finance”, or ReFi, movement, leveraging natural capital currencies and other tokenized natural assets. We’ve been finding that all of this is possible if we can reliably tie information about physical reality — where someone or something is, or measures of environmental conditions — to smart contracts, especially contracts capable of computational geometry.

Rather than working at the application layer, at Astral we are designing open source tools, public goods intended to underpin this category to A: make building location-based dapps easier, B: create spatial data storage systems fit for web3 (i.e. verifiable, uncensorable, permissionless, etc). We believe that if the ecosystem can converge on using these tools and design patterns, the location-based decentralized web will exhibit similar emergent composability that we’re witnessing in DeFi.

So what does this specifically mean?

* We’re developing **verifiable spatial data registries**, smart-contract based registries of vector or raster spatial data assets. Initially this was to store polygons representing geographic jurisdictions on chain, though we see use cases for points, lines, polyhedra and raster datasets as well. [More here →](https://ethereum-magicians.org/t/verifiable-spatial-data-registries/6688)
* We’ve also been designing a **verifiable location claim**, or a “universal location check-in”, a verifiable claim that serves as an attestation that someone / something was at a particular place at a particular time. This VC can be held privately by its creator, and submitted to any compatible location-based dapp or service. We are uncovering dimensions of trust, security and privacy, and that different applications will demand different procedures for creating these VCs.
* We’ve also built a proof-of-concept for a **Web3-native geospatial data storage system** on IPFS. This is for storing sensor data, which is key to many of the spatial finance applications we’ve been exploring like natural capital currencies, local / complementary / community currencies, parametric insurance, sustainability-linked bonds, carbon accounting systems etc. [More here →](https://docs.astral.global/develop/ipld-and-geotiffs)

### What Astral enables <a href="#what-astral-enables" id="what-astral-enables"></a>

As we see it, these primitives enable two key pieces of functionality:

#### Responding to ecological state changes <a href="#responding-to-ecological-state-changes" id="responding-to-ecological-state-changes"></a>

One is _tying smart contract behavior to ecological state changes_.

This is powerful technology, which makes it very dangerous. We are approaching the design and development of natural capital currencies with great humility. Initial thinking suggests that if we can look at a natural ecosystem from three perspectives. First, and most importantly by a large margin, from the people who live in, near and with the ecosystem, especially indigenous people. Supporting the human assessments of ecosystem state / health, we believe that data collected from proximate connected sensors deployed in the environment, along with remote sensing data captured from drones or satellites, can be analyzed to reach a reasonably accurate understanding of ecological conditions.

This is exciting because it means on-chain systems (DeFi, digital governance etc) can adapt to changes in ecosystem health, for example by rebasing a currency or tapping a community treasury to deploy capital when conditions approach threshold parameters. We are especially excited at the idea of detecting leading indicators of ecosystem degradation so we can support more targeted and less extreme interventions to preserve health.

#### Local contracts <a href="#local-contracts" id="local-contracts"></a>

The second: _local contracts_, smart contracts that can use location as a condition in its control flow, i.e. `require(pointInZone(coordinates, zoneGeometry))`, with the `coordinates` from a verifiable location claim and the `zoneGeometry` polygon stored in the verifiable spatial data registries. This binds smart contract behavior to spatial extents.

We believe with this functionality we can recreate tools of territorial governance that are the standard in the legacy system. We are working on [Spatial.sol](https://github.com/astralprotocol/spatial-sol), a suite of geometric and topological functions in Solidity. We’ve also designed and prototyped [a spatial governance protocol for connected devices](https://hyperaware.io), which could serve as a global (or, really, universal, within any spatial reference system) territorial governance system for self-sovereign jurisdiction administrators. Applications include e-mobility and intelligent transport, supply chain and logistics, autonomous vehicle governance and so on.

### Serving the universe and the metaverse <a href="#serving-the-universe-and-the-metaverse" id="serving-the-universe-and-the-metaverse"></a>

Astral is intended to underpin any dapps using spatial or location data. _This includes the metaverse._ In fact, we feel quite strongly that doing early experimentation and prototyping in the metaverse is the best way to understand and develop the technology.

This summary has focused on the technology, but we are placing a greater emphasis on people: on building the community of people who will be building with the public goods Astral is creating.

### Where we are heading <a href="#where-we-are-heading" id="where-we-are-heading"></a>

We've received funding as members of the [Climate Collective](https://climatecollective.org), and we’re engaging with thought leaders and prospective users to triangulate as versatile a design for these primitives as possible.

So — what do you think? What are we missing? Do you know of anyone working on related things? What should we be thinking about? Who might be interested — can you connect us?

Reach out on [Twitter](https://twitter.com/AstralProtocol) or join our [Discord](https://discord.gg/4WPyYvRtzQ)! ![:sparkles:](https://assets.hackmd.io/build/emojify.js/dist/images/basic/sparkles.png)
