[ Overview](./README.md)

![plot](./images/linkedin.png)


# Create an Invoice

An invoice is created to charge for services provided. Creating an invoice will result in a URL being available that should be sent to the customer. 
The customer follows the link to pay the invoice.

Once an invoice has been created, the invoice may be requested to get the details including its status.

Additionally (and optionally), webhook(s) may be registered to receive events on the progress of the invoice.

An invoice contains an `external_id`. This is an ID supplied by the PMS/Channel-partner. It must be unique for the
channel-partner and firm_id. This means that a channel partner needs to keep the external_id unique for the firm the 
invoice is created for. Invoices may be [retrieved using this ID](../../reference/partner-openapispec.yaml/paths/~1api~1v3~1partner~1invoices~1firm~1{firm_id}~1{external_id}/get) 
instead of the FeeWise generated ID 

### Pre-requisites
To create an invoice, on behalf of a Firm, using the partner api, the Firm must be active in FeeWise. 
If a Firm has not completed the onboarding process, creation of the invoice will fail with an error. 
Details of the Firm onboarding process can be found in the [FAQ](https://www.getfeewise.com/faq)

Details on the firm's status can be found in the [Firm Status Events](./ONBOARDING.md) documentation.

## Call endpoint to create the invoice


1. POST to [Create Invoice](../../reference/partner-openapispec.yaml/paths/~1api~1v3~1partner~1invoices/post).<br>Note the [Invoice](../../reference/partner-openapispec.yaml/components/schemas/Invoice) returned from the post contains the payment URL needed to pay the invoice.
2. Send the payment URL to the client.
3. Receive events on registered webhooks. (optional)
4. Make [GET requests on the invoice](../../reference/partner-openapispec.yaml/paths/~1api~1v3~1partner~1invoices~1{invoice_id}/get) to get the payment URL again. (optional)


### Example Create Invoice
```shell
curl --location --request POST 'https://papi.au.sandbox.getfeewise.com/api/v3/partner/invoices' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'X-CHANNEL-PARTNER-ID: 01786490-a44f-4c22-9ed6-cec4f9fde87b' \
--header 'X-API-KEY: 15ae4452-a6f8-411c-b49b-0cc8231b4a3d' \
--data-raw '{
  "firm_id": "7f623e2d-270d-8ad8-2e13-b7bfd022703e",
  "external_id": "e69f9433-885b-4321-bb48-9f5084850893",
  "amount": "123.45",
  "settlement_account": "Office",
  "external_reference": "inv-123",
  "currency": "AUD",
  "due_date": "1953-07-23T13:56:24.084Z",
  "description": "Charge for case setup",
  "matter": {
    "external_id": "my-unique-external-id",
    "external_reference": "my-external-reference",
    "description": "The matter of Frank vs Herman ",
    "type": "court"
  },
  "debtor": {
    "external_id": "case-client-1234",
    "name": "Frank",
    "email": "frank@email.com",
    "contact_number": "1300234567"
  },
  "line_items": [
    {
      "amount": "100",
      "name": "Phone call",
      "description": "Listened to voice message",
      "quantity": 1,
      "tax_rate": "10"
    },
    {
      "amount": "1000",
      "name": "Phone call",
      "description": "Replied to voice mail",
      "quantity": 1,
      "tax_rate": "15"
    }
  ],
  "notes": [
    "Got to know client",
    "Created initial case file"
  ],
  "payment_methods_override": [
    "Card"
  ]
}'
```

The response contains the id of the created invoice `"invoice_id": "2481ee61-283a-4d97-96ad-b2e50f929c96"`
```
{
    "invoice": {
        "amount": "123.45",
        "currency": "AUD",
        "debtor": {
            "contact_number": "1300234567",
            "email": "frank@email.com",
            "external_id": "case-client-1234",
            "name": "Frank"
        },
        "description": "Charge for case setup",
        "due_date": "1953-07-23T13:56:24.084Z",
        "external_id": "e69f9433-885b-4321-bb48-9f5084850893",
        "external_reference": "inv-123",
        "firm_id": "7f623e2d-270d-8ad8-2e13-b7bfd022703e",
        "invoice_id": "2481ee61-283a-4d97-96ad-b2e50f929c96",  # Note the invoice id in the response
        "line_items": [
            {
                "amount": "100",
                "description": "Listened to voice message",
                "name": "Phone call",
                "quantity": 1,
                "tax_rate": "10"
            },
            {
                "amount": "1000",
                "description": "Replied to voice mail",
                "name": "Phone call",
                "quantity": 1,
                "tax_rate": "15"
            }
        ],
        "matter": {
            "description": "The matter of Frank vs Herman ",
            "external_id": "my-unique-external-id",
            "external_reference": "my-external-reference",
            "type": "court"
        },
        "notes": [
            "Got to know client",
            "Created initial case file"
        ],
        "payment_methods_override": [
            "Card"
        ],
        "payment_uri": "https://au.sandbox.getfeewise.com/pay/2481ee61-283a-4d97-96ad-b2e50f929c96",
        "settlement_account": "Office",
        "status": "Submitted",
        "surcharge_choice_override": "Default"
    }
}
```

### Example Get Invoice

Using the id from  `create invoice` 

```shell
curl --location --request GET 'https://papi.au.sandbox.getfeewise.com/api/v3/partner/invoices/2481ee61-283a-4d97-96ad-b2e50f929c96' \
--header 'Accept: application/json' \
--header 'X-CHANNEL-PARTNER-ID: 01786490-a44f-4c22-9ed6-cec4f9fde87b' \
--header 'X-API-KEY: 15ae4452-a6f8-411c-b49b-0cc8231b4a3d'
```

Or using the external_id

```shell
curl --location --request GET 'http://papi.au.sandbox.getfeewise.com/api/v3/partner/invoices/firm/7f623e2d-270d-8ad8-2e13-b7bfd022703e/e69f9433-885b-4321-bb48-9f5084850893' \
--header 'Accept: application/json' \
--header 'X-CHANNEL-PARTNER-ID: 01786490-a44f-4c22-9ed6-cec4f9fde87b' \
--header 'X-API-KEY: 15ae4452-a6f8-411c-b49b-0cc8231b4a3d'
```

The response is the same as the response from the create


## Status state changes

| Status        | Meaning                                      |
|---------------|----------------------------------------------|
| Submitted     | The invoice has been accepted by the system. |
| Draft         | Currently unused                             |
| Authorised    | Currently unused                             |
| Voided        | Currently unused                             |


## Webhooks.

If real time updates are required, one or more webhooks must be registered for the topics for invoice processing. Note that 
a URL may be registered for each webhook or for many webhooks.

* invoice.created 
* invoice.updated


### invoice.created
Once the invoice has been created in the system, an event is POSTed to the URL registered for `invoice.created`.
The body is the [event envelop](../../reference/partner-openapispec.yaml/components/schemas/WebhookEvent) containing the created Invoice as the event payload.


### invoice.updated
Any change to the invoice after creation will result in an event being POSTed to the URL registered for `invoice.updated`.
The body is the [event envelop](../../reference/partner-openapispec.yaml/components/schemas/WebhookEvent) containing the created Invoice as the event payload.


