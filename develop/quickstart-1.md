---
description: Follow these simple steps to try Astral Protocol quickly
---

# Getting Started

## Setting up local Powergate Client

In order to store the GeoDIDs created by the core package, you will need to start up a local Powergate client or connect to an existing hosted client. Below will be a brief overview on how to setup a local Powergate client on your system. Further information is available at: [https://github.com/textileio/powergate](https://github.com/textileio/powergate).

{% hint style="info" %}
In order to setup the Powergate Client locally on your system you must have [Docker](https://docs.docker.com/engine/install/), [Docker-Compose](https://docs.docker.com/compose/install/), and [Go 1.16](https://golang.org/dl/) installed. 
{% endhint %}

In your terminal, create a new directory and clone the Powergate repo into it:

`git clone https://github.com/textileio/powergate.git`

After you clone the repo, enter the following commands:

`cd powergate/docker`

`make localnet`

More information regarding Powergate's Localnet mode, please refer to their documentation: [https://github.com/textileio/powergate\#localnet-mode](https://github.com/textileio/powergate#localnet-mode)

## Install the packages

```
yarn add @astralprotocol/core @astralprotocol/contracts dotenv bs58 truffle @truffle/hdwallet-provider
```

## Configure truffle-config.js

```bash
const HDWalletProvider = require("@truffle/hdwallet-provider");
require('dotenv').config();

// Create a .env file with your MNEMONIC and a ROPSTEN API key from INFURA
// Must have the following format:
// MNEMONIC="words here "
// ROPSTEN_API_KEY=https://ropsten.infura.io/v3/key

let mnemonic = process.env.MNEMONIC
let ropstenURL = process.env.ROPSTEN_API_KEY


let provider = new HDWalletProvider({
  mnemonic: {
    phrase: mnemonic,
  },
  providerOrUrl: ropstenURL,
});

module.exports = {
  networks: {
    development: {
      host: "127.0.0.1",
      port: 8545,
      network_id: "*",
    },
    ropsten: {
      provider: provider,
      network_id: "3",
    },
  },
  compilers: {
    solc: {
      version: "0.6.12",
    },
  },
};

```

## Create a script for interacting with the Astral Client and Contracts

{% code title="scripts/deployGeoDIDs.js" %}
```bash
const { AstralClient } = require('@astralprotocol/core');
const SpatialAssets = require("@astralprotocol/contracts/build/contracts/SpatialAssets.json")
const bs58 = require('bs58')

module.exports = async function (callback) {
  const stringToBytes = (string) => web3.utils.asciiToHex(string)

    // based on https://ethereum.stackexchange.com/questions/17094/how-to-store-ipfs-hash-using-bytes32
  // Return bytes32 hex string from base58 encoded ipfs hash,
  // stripping leading 2 bytes from 34 byte IPFS hash
  // Assume IPFS defaults: function:0x12=sha2, size:0x20=256 bits
  // E.g. "QmNSUYVKDSvPUnRLKmuxk9diJ6yS96r1TrAXzjTiBcCLAL" -->
  // "0x017dfd85d4f6cb4dcd715a88101f7b1f06cd1e009b2327a0809d01eb9c91f231"
  function getBytes32FromIpfsHash(ipfsListing) {
    return "0x"+bs58.decode(ipfsListing).slice(2).toString('hex')
  }

  try {

    const accounts = await web3.eth.getAccounts()
    const userAccount = accounts[0]

    // find contract in network 3 (Ropsten)
    const SpatialAssetsContract = new web3.eth.Contract(SpatialAssets.abi, SpatialAssets.networks['3'].address, {
      from: userAccount,
      data: SpatialAssets.deployedBytecode,
    });

    // update the endpoint to the latest
    const subgraphEndpoint = "https://api.thegraph.com/subgraphs/name/astralprotocol/spatialassetsv07"
  
    const astral = new AstralClient(userAccount, subgraphEndpoint);
  
    const storage = stringToBytes('FILECOIN');
    // Enable a storage first

    try {
      await SpatialAssetsContract.methods.enableStorage(storage).send()
      .on('receipt', function(receipt){
        // receipt example
        console.log(receipt);
  
      })
      .on('error', function() { // If the transaction was rejected by the network with a receipt, the second parameter will be the receipt.
        console.log('Already enabled storage: ' + storage);
      });
    } 
    catch (err) {
      // Will throw an error if storage is already active
      console.log(err)
    }

  
    // Creates a Genesis GeoDID 
    
    const genDocRes = await astral.createGenesisGeoDID('collection')
    console.log(genDocRes);
  
    // With the returned IDocumentInfo from the last function, we can pin it.
    // Since no token was specified the client will assign a new auth Token to the user.
    
    const results = await astral.pinDocument(genDocRes);
    console.log(results);
    
    const token = results.token;
          
    // register the geodid id and cid obtained. Type 0 because it is a collection

    console.log(results.geodidid)
    console.log(results.cid)

    const bytes32GeoDID= getBytes32FromIpfsHash(results.geodidid.substring(8));
    const bytes32Cid = getBytes32FromIpfsHash(results.cid);
  
    try {
      await SpatialAssetsContract.methods.registerSpatialAsset(userAccount, bytes32GeoDID, stringToBytes(''),[], bytes32Cid, storage,0).send()    
      .on('receipt', function(receipt){
      // receipt example
      console.log(receipt);

      })
      .on('error', function(error) { // If the transaction was rejected by the network with a receipt, the second parameter will be the receipt.
        console.log(error);
      });
    } 
    catch (err) {
      // Will throw an error if tx reverts
      console.log(err)
    }

    
    // With the Auth Token and the GeoDID ID we can load the document with the loadDocument function
    const loadResults = await astral.loadDocument(results.geodidid, token);
    console.log(loadResults);

  }
  catch(error) {
    console.log(error)
  }

    callback()
};
```
{% endcode %}

```bash
"deployGeoDIDs": "truffle exec scripts/deployGeoDIDs.js --network ropsten",
```

## And execute with

```bash
yarn deployGeoDIDs
```

{% hint style="info" %}
**The steps executed in this page have been reproduced in a public github that you can consult:**  
  
[**https://github.com/AstralProtocol/wrapperTest**](https://github.com/AstralProtocol/wrapperTest)\*\*\*\*
{% endhint %}

