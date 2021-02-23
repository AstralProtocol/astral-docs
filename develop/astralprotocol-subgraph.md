---
description: Documentation about the Astral Protocol Subgraph Package.
---

# @astralprotocol/subgraph

## **Description**

The **@astralprotocol/subgraph** serves as the indexing engine of the protocol, capturing the registration and modification events of GeoDIDs in the [**@astralprotocol/contracts**](docs/)**.** It acts like a decentralized querying database where it is substantially easier to make complex queries to the Spatial Assets registry. It is used to create the tree of GeoDID nodes that represents their relationships and groupings.

The current version of the subgraph \(**v03**\) is indexing the Ethereum **Roptsten** network at the following GraphQL endpoints:

```text
https://api.thegraph.com/subgraphs/name/astralprotocol/spatialassetsv03
wss://api.thegraph.com/subgraphs/name/astralprotocol/spatialassetsv03
```

You can connect to these with your GraphQL client of choice or try them at [The Graph's playground](https://thegraph.com/explorer/subgraph/astralprotocol/spatialassetsv03).

## **To add Astral Protocol Subgraph to your application**

```text
yarn add @astralprotocol/subgraph
```

## **To develop or try the Astral Protocol Subgraph locally**

#### Prerequisites

* Clone the astralprotocol repository and go to packages/subgraph

  `sudo apt-get install libsecret-1-dev`

* [Docker Instalation](https://docs.docker.com/install/linux/docker-ce/debian/)
* `git clone https://github.com/graphprotocol/graph-node/` \(check setup instructions for docker version  on [https://thegraph.com/docs/](https://thegraph.com/docs/)\)

#### Deployment

1. Run ganache, in a separate terminal with the script in package.json \(root folder\): `yarn ganache`
2. Deploy contracts from  `@astralprotocol/contracts` with `yarn truffle` in the root folder. Update addresses in the `subgraph.yaml` if needed and ensure the correct file is named according to the network of deployment \(for ganache it should read as mainnet - backup the current `subgraph.yaml` file and rename `subgraphLocal.yaml`\).
3. In a third terminal, inside the graph-node folder, run `cd docker && docker-compose up`. If using Docker for WSL, Docker must be running on Windows. If graph-node throws an error try clearing the `data/postgres` folder, within the docker directory of graph-node, with `sudo rm -rf data/postgres`. Restart docker if needed.
4. Generate subgraph typescript files with `yarn codegen`, then create and deploy the subgraph to the graph-node with `yarn create-local && yarn deploy-local`
5. You can query the subgraph and view the GeoDID tree in the local provided endpoint.

#### Testing

The following query can be provided to the graphql endpoint to view the GeoDIDs tree \(after doing the deployment steps above\):

```text
{
  geoDIDs {
    id
    owner
    cid
    storage
    root
    parent
    edges {
      id
      childGeoDID {
        id
      }
    }
    active
    type
  }
}
```

