---
description: Framing our work at Astral
---

# Introduction

At Astral we are creating the tools developers will need to build an ecosystem of location-based dApps and composable spatial contracts. We see a vast opportunity space here, with exciting early initiatives from [FOAM](https://foam.space/), [Regen Network](https://www.regen.network/), [Grassroots Economics](https://www.grassrootseconomics.org/), [IoTeX](https://iotex.io/), [IBISA Network](https://ibisa.network/) and others.

Our vision at Astral is to build tools and help establish standards that will enable a composable location-based decentralized web. We're quite early in our journey, and have an orienting question prompting these investigations - what if we could use an entity's physical location as a condition in a smart contract? And relatedly, how can we connect verifiable insights about physical reality with smart contract logic?

Our investigations into this question has hardened our understanding of the tools and components needed. Our goal here is to share these ideas openly - gather some feedback, and see if you or anyone you know would be interested in supporting one or more of these initiatives with expertise and / or capital. Our strategy is to design a modular architecture of Web3 spatial primitives - each useful in their own right, but designed to function best together.

We have built a few Astral dApp prototypes, and have architected a few more. This work has helped us identify versatile tools that would have accelerated development, regardless of the application. Based on these insights we are conceptualizing the design space as a three layer stack.

* **Spatial Contracts** - smart contracts that use location or spatial data in some way
* **Data** - capture, storage and perhaps processing 
* **Oracles** - to connect the two

Our goal is to produce a suite of tools, libraries and SDKs that would let developers efficiently build location-based dapps without having to deal with the complexities of managing spatial data in the Web3 paradigm. A second order effect is that if the community adopts standards, applications become composable.

To achieve this goal, we are currently working on a few initiatives:

* [Spatial.sol](spatial.sol.md), a Solidity library of topological and geometric functions
* [Verifiable spatial data registries](verifiable-spatial-data-registries.md)
* [GeoDIDs](geodids.md)
* [IPLD-encoded raster and vector spatial datasets](../develop/ipld-and-geotiffs/)
* [Spatial oracles](oracles.md)
* [Universal location proofs](universal-location-proofs.md)

