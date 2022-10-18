# List on Ocean Marketplace

<figure><img src="../../../.gitbook/assets/list (1).png" alt=""><figcaption><p>Listing query data on Ocean marketplace highlighted</p></figcaption></figure>

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

Data from the second query was listed on the Ocean Görli test network:

* [Sample query test listing](https://market.oceanprotocol.com/asset/did:op:cc3b1f3c38110b303ece32fa7d56ef11921d61a4d48e8793c3b5e1959773f08c)
* [Data NFT ](https://testnets.opensea.io/assets/goerli/0x3414f8e9f479a3a8305d0808ce84a46b5d351fef/1)on Opensea Görli Testnet&#x20;

Note that you need Görli ETH and Görli OCEAN tokens to purchase. [Faucet for Görli OCEAN](https://faucet.goerli.oceanprotocol.com/)

### Relevant code:

* [Sample client query](https://github.com/MRV-Studio/openmrv-server/blob/main/src/test/avg.query.ts)
* [Public endpoint](https://github.com/MRV-Studio/openmrv-server/blob/main/src/controller/public.controller.ts)
