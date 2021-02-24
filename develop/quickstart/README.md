---
description: Documentation about the Astral Protocol Core Package.
---

# @astralprotocol/core

## Description

The **@astralprotocol/core** package is a Typescript NPM package that is responsible for any CRUD operations performed on the DID Documents. This includes the creation of DID Documents, loading the DID Documents, as well as updating them. The package also has utilities that enable the creation of the collision resistant GeoDID IDs, a custom ****[**did-resolver**](https://github.com/decentralized-identity/did-resolver) that enables DID Resolution, as well as pinning features for storing the Documents on IPFS or FFS. This package is meant to be used in conjunction with the [**@astralprotocol/contracts**](../docs/) ****and [**@astralprotocol/subgraph**](../astralprotocol-subgraph.md) ****packages. However, the package can also be used independently if the user does not want to rely on the Ethereum network.

{% hint style="info" %}
This package is not responsible for persistence of the documents \(mappings, etc.\), the created DID Documents are persisted through IPFS/FFS, and the metadata regarding the DID Documents are persisted through the subgraph and smart contracts.
{% endhint %}

## **To add Astral Protocol Core to your application**

```text
yarn add -D @astralprotocol/core
OR
npm install -D @astralprotocol/core

import AstralClient from '@astralprotocol/core';
OR
const AstralClient = require('@astralprotocol/core');
```

## **To develop or try the Astral Protocol Core locally**

* **Step 1**
* **Step 2**
* **Step 3**

**Example Implementation of core package:**

```text
import AstralClient from '@astralprotocol/core';

async function run(){

    // Create a new Astral Client Instance with the user's ethAddress
    let astral = new AstralClient('0xa3e1c2602f628112E591A18004bbD59BDC3cb512');
    
    try{
    
        // Creates a Genesis GeoDID 
        const genDocRes = await astral.createGenesisGeoDID('collection')
        console.log(genDocRes);

        // With the returned IDocumentInfo from the last function, we can pin it.
        // Since no token was specified the client will assign a new auth Token to the user.
        const results = await astral.pinDocument(genDocRes);
        console.log(results);

        const token = results.token;

        // With the Auth Token and the GeoDID ID we can load the document with the loadDocument function
        const loadResults = await astral.loadDocument(results.geodidid, token);
        console.log(loadResults);

        console.log('\n');
        console.log('\n');

        // Creates a Child GeoDID Item of the priviously created Genesis GeoDID
        const itemres = await astral.createChildGeoDID('item', results.geodidid, 'item1');
        console.log(itemres)

        console.log('\n');

        // With the returned IDocumentInfo from the last function, we can pin it.
        // This time we reuse the same token that was created earlier to pin the child document to the same instance.
        const itemresults = await astral.pinDocument(itemres, token);
        console.log(itemresults);

        console.log('\n');

        // With the Auth Token and the GeoDID ID we can load the document with the loadDocument function
        const loadItemResults = await astral.loadDocument(itemresults.geodidid, token);
        console.log(loadItemResults);

        console.log('\n');

        // Here we can display the string representation of the DID Document
        console.log(JSON.stringify(loadItemResults.documentInfo.documentVal));

    }catch(e){
        console.log(e);
    }
    
}
```

#### 

