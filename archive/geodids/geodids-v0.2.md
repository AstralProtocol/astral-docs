---
description: Planned upgrades to the GeoDID Method Specification
---

# GeoDIDs v0.2

GeoDIDs identify spatial data assets. DIDs support selectors, paths, query parameters and fragments. These additional details that can be included in a GeoDID offer a powerful way to efficiently represent and store large spatial datasets in a much more resource-constrained manner that is still persistent, cryptographically verifiable and optionally private.

The next phase of research and development will be for GeoDIDs that support spatial querying and clipping. 

For example, consider GeoDID representing a collection of satellite imagery. We should be able to specify a sub-collection, or even item, that defines a spatial and temporal query in the GeoDID itself. That way, a user could store a single GeoDID that specifies a single image, clipped to a particular area, extracted from the GeoDID Collection. The user would not need to store that clipped image, but only the GeoDID with query parameters - they would still have the confidence that the GeoDID would resolve to the same clipped image permanently. 

This would be crucial for the auditability of spatial finance applications. A satellite image might prove that a particular green infrastructure project was completed by a certain date, or that some insured natural capital warranted a payout. For both traditional and decentralized spatial finance, this verifiability will likely bring a lot of value to 

See [Decentralized Identifiers](https://www.windley.com/archives/2019/02/decentralized_identifiers.shtml) by Dr Phil Windley for more details on selectors, paths, query parameters and fragments.

