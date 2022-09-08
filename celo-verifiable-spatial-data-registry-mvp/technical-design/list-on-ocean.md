# List on Ocean

<figure><img src="../../.gitbook/assets/list (1).png" alt=""><figcaption><p>Listing query data on Ocean marketplace outlined</p></figcaption></figure>



The sample queries take a polygon, date range, and provider id and return the average temperature, and the raw data points, respectively. The query endpoints are public so no access token is required to run:

```bash
# sample analytics query:
# query one month's 3 hourly data for a polygon and provider, return average temperature.
export HOST=https://<host>.com/api
curl -s \
     -w '\n' \
     -G \
     -H "Content-Type: application/json" \
     -d 'polygon={"type":"Polygon","coordinates":[[[-3.7025,40.4165],[3,60],[6,90],[-3.7025,40.4165]]]}' \
     -d 'startdate=2019-01-01' \
     -d 'enddate=2019-01-02' \
     -d 'providerId=tSuqRPkLVfDqQG3mgr0x4' \
     $HOST/596090/00833a
# raw data on which above query is based:
curl -s \
     -w '\n' \
     -G \
     -H "Content-Type: application/json" \
     -d 'polygon={"type":"Polygon","coordinates":[[[-3.7025,40.4165],[3,60],[6,90],[-3.7025,40.4165]]]}' \
     -d 'startdate=2019-01-01' \
     -d 'enddate=2019-01-02' \
     -d 'providerId=tSuqRPkLVfDqQG3mgr0x4' \
     $HOST/596090/7afb79
```

The data query is more appropriate for the Ocean marketplace than the previous average temperature query, which is more an example of a composable intermediate endpoint for an inference toolchain.

Data from the second query was listed on the Ocean Rinkeby test network: [Sample query test listing](https://market.oceanprotocol.com/asset/did:op:6408cb610c9efec38055ccbcaa4dfd6a2e4ff03e95bbf202e4b612a88ac025a5)&#x20;

Note that you need Rinkeby ETH and Rinkeby OCEAN tokens to purchase.

### Relevant code:

* [Sample client query](https://github.com/MRV-Studio/openmrv-server/blob/main/src/test/avg.query.ts)
* [Public endpoint](https://github.com/MRV-Studio/openmrv-server/blob/main/src/controller/public.controller.ts)
