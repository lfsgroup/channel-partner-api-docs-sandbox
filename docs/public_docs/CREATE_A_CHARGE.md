[ Overview](./README.md)

![plot](./images/linkedin.png)


# Charges
A charge is a generic FeeWise artifact that allows a PMS to bill a firm's client for services provided.

# Create a charge - Existing FeeWise Customer
Firms will be able to create a charge for an existing FeeWise customer. (A customer that has already made a charge payment, via FeeWise)

The process for creating a charge for an existing customer is as follows:
* The FeeWise API is used to retrieve the Firm's customers and their stored payment method. (as a tokenised value)
* The PMS user selects a customer and the payment method to use. (token)
* The PMS utilises the chosen customer's payment method token to initiate and execute a charge against the selected payment method.

# Create a charge - New Customer
If the customer is new to FeeWise, the process is as follows:

* The PMS initiates a payment token request, specifying whether the payment token should be single-use or multi-use.
* After generating the token, a URI is provided, denoting the location of the FeeWise hosted fields app. This app is hosted within an iframe by the PMS and is utilised for the collection of payment details.
* After collecting payment details, the payment token is stored in FeeWise along with necessary payment method details, enabling the payment method to be utilised for subsequent charges.
* Utilising the stored payment token, the PMS is capable of creating and processing charges directly.
  

Once a payment has been created, the Charge may be requested to get the details including its status.

Additionally (and optionally), webhook(s) may be registered to receive events on the progress of the charge.

a charge contains an `external_id`. This is an ID supplied by the PMS/Channel-partner. It must be unique for the
channel-partner and firm_id. This means that a channel partner needs to keep the external_id unique for the firm the
charge is created for. Charges may be [retrieved using this ID](../../reference/partner-openapispec.yaml/paths/~1api~1v3~1partner~1charges~1firm~1{firm_id}~1{external_id}/get)
instead of the FeeWise generated ID

