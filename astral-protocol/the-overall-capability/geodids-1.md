# Data

Spatial data comes in many different formats, from myriad sources, containing different information. As Astral wants to make as few assumptions as possible about the use cases that the protocol will be used for, we are leaving room for devs to work with any spatial data formats - including ones that haven't been developed yet.

To achieve this, and to make sure that spatial data used in Astral is reliable and controlled by the user, we are designing a [DID Method ](https://w3c.github.io/did-core)specifically for identifying spatial data assets. 

The [GeoDID Method Specification ](../../geodids/geodid-core-specification/)will act as the default Web3 specification for working with geo-spatial data sets. Each DID Document will reference one or many spatial data assets endpoints and its respective metadata.  The core spec is very lightweight - support for different formats are built in as Extensions. 

GeoDIDs are designed to work with any spatial data assets, leaving the user to decide if they trust the data identified. We are designing best practices and advanced extensions that will help data consumers trust that satellite imagery is not tampered with, that locations are trustworthy and so on. 

Learn more about DIDs and GeoDIDs here:

{% page-ref page="../../geodids/dids.md" %}

{% page-ref page="../../geodids/geodid-intro/" %}



