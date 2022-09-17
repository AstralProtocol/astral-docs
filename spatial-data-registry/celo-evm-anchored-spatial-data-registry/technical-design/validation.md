# Validation

<figure><img src="../../../.gitbook/assets/validation (1).png" alt=""><figcaption><p>Validation process highlighted</p></figcaption></figure>

The validation process, running under the 'validator' role, retrieves a requested number of unvalidated anchors, and for each one, retrieves the associated data points, recalculates the summary hash.&#x20;

The current counts and hash results are then compared to both the Celo contract and database counts and hash results established by the anchor process and any discrepancies are reported.

### Relevant code:

* [Validation endpoint](https://github.com/MRV-Studio/openmrv-server/blob/main/src/controller/validatorController.ts)
* [Validation service](https://github.com/MRV-Studio/openmrv-server/blob/main/src/service/validator.service.ts)
* [Contract service](https://github.com/MRV-Studio/openmrv-server/blob/main/src/service/contract.service.ts)
* [Celo Contract](https://github.com/MRV-Studio/openmrv-contract/blob/main/contracts/GeodataAnchor.sol)
* [Contract anchor and validation integration test](https://github.com/MRV-Studio/openmrv-server/blob/main/src/test/localnode.test.ts)
