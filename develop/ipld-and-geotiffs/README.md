---
description: >-
  Testing whether we could use IPLDs DAG-DBOR encoding and IPFS to compliment
  the Internal File Directory(IFD), for the TIFF file.
---

# GeoTIFFs and IPLD

## Introduction

One of Astral's main tenets, was to bring cloud native Geospatial capabilities to the Web3 space. While working with Protocol Labs tech for the past few months, we gained some insight into how, IPLD data structures, libp2p, IPFS, FFS, can enable us to make the aforementioned a reality. 

We knew we had to experiment with different pieces of tech, in order to understand what's possible, and what we could do to improve the existing tools. With Raster Imagery being so important to the Geospatial community, we challenged ourselves to figure out how we could  bring Cloud Optimized GeoTIFF-esque type functionality to IPFS/FFS. 

### **What is a Cloud Optimized GeoTIFF?**

A [Cloud Optimized GeoTIFF \(COG\)](https://www.cogeo.org/) is a regular GeoTIFF file, aimed at being hosted on a HTTP file server, with an internal organization that enables more efficient workflows on the cloud. It does this by leveraging ​HTTP GET range requests to ask for just the parts of a file the client needs. “COG is the ideal pair for a STAC Item” - the two standards were designed to complement one another.

By pre-processing the GeoTIFF and breaking it into several pieces, a number of internal ‘tiles’ are created inside the actual image, instead of using simple ‘stripes’ of data. With tiles, much quicker access to a certain area is possible, so that just the portion of the file that needs to be read is accessed.

In addition, during the pre-processing, multiple ‘overviews’ will be computed and incorporated into the image file - basically several downsampled versions of the same image - so that you can query the highest quality version depending on the level of resolution desired.

In order to achieve this, the client uses HTTP GET Range requests to request the range of bytes that are within the zoom scope, from the server. This method is also called byte serving, where the client can request just the bytes that it needs from the server. On the broader web it is very useful for serving things like video, so clients don’t have to download the entire file to begin playing it.

### Replacing the GeoTIFFs IFD with IPLD

Essentially our goal is to take a GeoTIFF \(that is a STRIPE image in this stage\), pre-process the image by tiling the STRIPE image and then creating the respective overviews for each tile. Instead of the tiles and overviews being stored in the TIFFs IFD \(Image File Directory\), we’re thinking we can use IPLD to store the tiles and overviews instead. With each tile/overview having their own CID, we can then use  to query the proper tiles/overviews. 

In theory it sounds like it would work, and we know there will be some downsides to this approach \(speed, efficiency, and lack of adoption for right now\). But we would still like to see where this could go and if IPLD could be used to enable CID GET Range requests for geospatial raster data. 

## Mental Model

TODO: explain the mental model of this approach 



![Visualization](../../.gitbook/assets/screen-shot-2020-12-04-at-9.39.52-am.png)

## Conclusion

### How we plan to further our research?

In order to further our research, we would like to develop an IPLD-encoded GeoTIFF, which can hopefully be extended to provide byte serving capabilities to other files types as well. We think we can do this by developing a custom IPLD codec that is specifically meant for TIFF filetypes. We can encode the GeoTIFF, by breaking the GeoTIFF into tiles and their respective overviews, encoding it with our custom codec, which should tag the CIDs of the tiles, so we can enable "byte serving capabilities".

Instead of using HTTP GET Range requests, we can enable CID GET Range requests, where the selected/targeted bytes are encoded within the CID, for ease of access from the client. We’re thinking that we can accomplish this by the use of IPLD selectors. This will enable a more effective way to query data from IPFS by significantly reducing downloading times, costs, and resource use - and serve as a step towards IPFS-native geospatial technology.

#### We plan to focus on the following:

* Chunking and Distribution of Large Files
* Real Time & Dynamic Processing
* Minimize Data Duplication
* See if Custom Codec is necessary, or if DAB-CBOR still suffices
* Leverage IPLD Selectors to query data efficiently.



