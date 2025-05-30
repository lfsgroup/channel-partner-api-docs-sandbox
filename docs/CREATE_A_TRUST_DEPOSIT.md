[ Overview](./README.md)

![plot](./images/linkedin.png)


# Create a Trust Deposit

A trust deposit is created to request money be paid into a trust. Creating a trust deposit will result in a URL being available that should be sent to the customer. 
The customer follows the link to pay into the trust.

Once an trust deposit has been created, the trust deposit may be requested to get the details including its status.

Additionally (and optionally), webhook(s) may be registered to receive events on the progress of the trust deposit.

A trust deposit contains an `external_id`. This is an ID supplied by the PMS/Channel-partner. It must be unique for the
channel-partner and firm_id. This means that a channel partner needs to keep the external_id unique for the firm the
trust deposit is created for. Invoices may be [retrieved using this ID](../../reference/partner-openapispec.yaml/paths/~1api~1v3~1partner~1trust-deposits~1firm~1{firm_id}~1{external_id}/get)
instead of the FeeWise generated ID

### Pre-requisites
To create a Trust Deposit, on behalf of a Firm, using the partner api, the Firm must be active in FeeWise.
If a Firm has not completed the onboarding process, creation of the Trust Deposit will fail with an error.
Details of the Firm onboarding process can be found in the [FAQ](https://www.getfeewise.com/faq)

Details on the firm's status can be found in the [Firm Status Events](./ONBOARDING.md) documentation.

## Call endpoint to create the trust deposit


1. POST to [Create Trust Deposit](../../reference/partner-openapispec.yaml/paths/~1api~1v3~1partner~1trust-deposits/post).<br/>Note the [TrustDeposit](../../reference/partner-openapispec.yaml/components/schemas/TrustDeposit) returned from the post contains the payment URL needed to pay into the trust account.
2. Send the payment URL to the client.
3. Receive events on registered webhooks. (optional)
4. Make [GET requests on the trust deposit](../../reference/partner-openapispec.yaml/paths/~1api~1v3~1partner~1trust-deposits~1{trust_deposit_id}/get) to get the payment URL again. (optional)



### Example Create Trust Deposit

```shell
curl --location --request POST 'https://papi.au.sandbox.getfeewise.com/api/v3/partner/trust-deposits' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'X-CHANNEL-PARTNER-ID: 01786490-a44f-4c22-9ed6-cec4f9fde87b' \
--header 'X-API-KEY: 15ae4452-a6f8-411c-b49b-0cc8231b4a3d' \
--data-raw '{
  "firm_id": "7f623e2d-270d-8ad8-2e13-b7bfd022703e",
  "external_id": "e69f9433-885b-4321-bb48-9f5084850893",
  "amount": "123.45",
  "external_reference": "inv-aaa",
  "currency": "AUD",
  "due_date": "1953-07-23T13:56:24.084Z",
  "description": "Charge for case setup",
  "matter": {
    "external_id": "my-unique-external-id",
    "external_reference": "my-external-reference",
    "description": "The matter of Frank vs Herman",
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

The response contains the id of the created trust deposit `"trust_deposit_id": "395bac64-14ab-43bc-abdd-7bbb79ca9a2f"`
```
{
    "trust_deposit": {
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
        "external_reference": "inv-aaa",
        "firm_id": "7f623e2d-270d-8ad8-2e13-b7bfd022703e",
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
            "description": "The matter of Frank vs Herman",
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
        "payment_uri": "https://au.sandbox.getfeewise.com/pay/395bac64-14ab-43bc-abdd-7bbb79ca9a2f",
        "status": "Submitted",
        "surcharge_choice_override": "Default",
        "trust_deposit_id": "395bac64-14ab-43bc-abdd-7bbb79ca9a2f"
    }
}


```

### Example Get Trust Deposit

Using the id from  `create trust deposit`

```shell
curl --location --request GET 'https://papi.au.sandbox.getfeewise.com/api/v3/partner/trust-deposits/395bac64-14ab-43bc-abdd-7bbb79ca9a2f' \
--header 'Accept: application/json' \
--header 'X-CHANNEL-PARTNER-ID: 01786490-a44f-4c22-9ed6-cec4f9fde87b' \
--header 'X-API-KEY: 15ae4452-a6f8-411c-b49b-0cc8231b4a3d'
```

Or using the external_id

```shell
curl --location --request GET 'http://papi.au.sandbox.getfeewise.com/api/v3/partner/trust-deposits/firm/7f623e2d-270d-8ad8-2e13-b7bfd022703e/e69f9433-885b-4321-bb48-9f5084850893' \
--header 'Accept: application/json' \
--header 'X-CHANNEL-PARTNER-ID: 01786490-a44f-4c22-9ed6-cec4f9fde87b' \
--header 'X-API-KEY: 15ae4452-a6f8-411c-b49b-0cc8231b4a3d'
```

The response is the same as the response from the create



## Status state changes

| Status        | Meaning                                            |
|---------------|----------------------------------------------------|
| Submitted     | The trust deposit has been accepted by the system. |
| Draft         | Currently unused                                   |
| Authorised    | Currently unused                                   |
| Voided        | Currently unused                                   |


## Webhooks.

If real time updates are required, one or more webhooks must be registered for the topics for invoice processing. Note that 
a URL may be registered for each webhook or for many webhooks.

* trust_deposit.created 
* trust_deposit.updated


### trust_deposit.created
Once the trust deposit has been created in the system, an event is POSTed to the URL registered for `trust_deposit.created`.
The body is the [event envelop](../../reference/partner-openapispec.yaml/components/schemas/WebhookEvent) containing the created [TrustDeposit](../../reference/partner-openapispec.yaml/components/schemas/TrustDeposit) as the event payload.


### trust_deposit.updated
Any change to the trust deposit after creation will result in an event being POSTed to the URL registered for `trust_deposit.updated`.
The body is the [event envelop](../../reference/partner-openapispec.yaml/components/schemas/WebhookEvent) containing the created [TrustDeposit](../../reference/partner-openapispec.yaml/components/schemas/TrustDeposit) as the event payload.


