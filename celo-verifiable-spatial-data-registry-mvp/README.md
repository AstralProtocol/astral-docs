# Celo Verifiable Spatial Data Registry MVP



## Introduction

The purpose of this MVP was to demonstrate a workflow from an MRV data provider, supplying raw measurement data based on both stationary and mobile sources, to a backend with the following features:

* an ingestion process including:
  * timeseries and geospatial location (both point and polygon-based) indexing
  * a flexible data schema to accommodate multiple data types and units of measure
  * hashing of raw measurement data on ingestion
* an anchoring process including:
  * summary hashing of data hashes
  * anchoring of summaries to the database and Celo blockchain
* a validation process verifying the hashing and anchoring processes
* account-based authentication and authorization, separating the above functionality by role
* a means to create a public HTTP endpoint to list the results of queries on the Ocean marketplace
* a test layer covering the above functionality
