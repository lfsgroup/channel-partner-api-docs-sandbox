[ Overview](./README.md)
![plot](./images/linkedin.png)

# Changelog
The FeeWise api is continuously being improved with new features, bug fixes and documentation updates. Details of the changes will be added to the changelog as they are released 

## September 2022

* Payments
  * Added API [getPayments](../../reference/partner-openapispec.yaml/paths/~1api~1v3~1partner~1payments~1/get) endpoint to allow for retrieval of payments by various search criteria. NB API only, not yet implemented
  * Added API [recordExternalPayment](../../reference/partner-openapispec.yaml/paths/~1api~1v3~1partner~1payments~1external~1/post) to allow payments made externally to feewise to be recorded. NB API only, not yet implemented
  
* Payouts
  * AddedAPI  [getPayouts](../../reference/partner-openapispec.yaml/paths/~1api~1v3~1partner~1payouts~1/get) endpoint to allow for retrieval of payouts by various search criteria. NB API only, not yet implemented
  
## July 2022

* Artifacts
  * Added /create-invoice endpoint
  * Added /create-trust-deposit endpoint

* Webhooks
  * Added /webhooks CRUD endpoints
  * Added HMAC Signatures to responses
  * Added /events endpoint
  * Added /events/replay/{eventID} endpoint
  * Added /events/types endpoint

## June 2022
Initial version
