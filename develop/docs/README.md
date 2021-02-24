---
description: Documentation about the Astral Protocol Contracts Package.
---

# @astralprotocol/contracts

[![Build Status](https://www.travis-ci.com/AstralProtocol/astralprotocol.svg?branch=master)](https://www.travis-ci.com/AstralProtocol/astralprotocol) [![Coverage Status](https://coveralls.io/repos/github/AstralProtocol/astralprotocol/badge.svg?branch=master)](https://coveralls.io/github/AstralProtocol/astralprotocol?branch=master)

## **Description**

These contracts serve as the Registry for the Astral Protocol GeoDIDs. It allows binding of a GeoDID to an ethereum address and CID name resolving.

By registering a spatial asset Smart Contract events are triggered, which are picked up by the subgraph indexer to build the tree of relationships for easy querying.

## **To add Astral Protocol Contracts to your application**

```text
yarn add @astralprotocol/contracts
```

## **To develop or try the Astral Protocol Contracts locally**

* Clone the [astralprotocol repository](https://github.com/AstralProtocol/astralprotocol) and go to packages/contracts:

```text
git clone git@github.com:AstralProtocol/astralprotocol.git
cd astralprotocol/packages/contracts
```

* Run ganache `yarn ganache`
* In a new terminal, deploy contracts with `yarn truffle`
* Run tests with `yarn truffle-test` 
* You can deploy an instance by running `yarn new-instance`. It builds a GeoDID tree with hardcoded GeoDID ids and CIDs.
* You can test the removal of some links by running `yarn remove-links`.
* Watch the changes in a locally deployed [subgraph](../astralprotocol-subgraph.md).
* Do coverage check up by killing the `ganache` process in the first terminal and running `yarn coverage`

## **To deploy your own contracts in the Ropsten testnet**

* Create a `.env` file in `/packages/contracts` with a `MNEMONIC` and `ROPSTEN_API_KEY`

{% code title=".env" %}
```text
MNEMONIC="mnemonic phrase goes here with testnet ether in address[0] on ropsten cool"
ROPSTEN_API_KEY=https://ropsten.infura.io/v3/<PROJECT ID HERE>
```
{% endcode %}

