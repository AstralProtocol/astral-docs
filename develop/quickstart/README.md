---
description: Description and quick-start
---

# @astralprotocol/core

**To get started with the Astral Core Package:**

`yarn add @astralprotocol/core`

`npm install @astralprotocol/core`

**Import the package into your project:**  
`import AstralClient from '@astralprotocol/core';`

`const AstralClient = require('@astralprotocol/core');`

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

