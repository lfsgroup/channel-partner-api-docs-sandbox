# API Roadmap

The API and platform is currently under heavy development at this time (September 2022) and is not production ready yet. 
We're targeting a Dec 2022 go-live with production ready APIs at this time.

## Current Status

## Environment
The current available environment is a [sandbox environment](./SANDBOX.md). This may be used for testing and Channel 
Partners can be onboarded to this platfrom on request


## API
The API should be considered beta quality. Breaking and non-breaking changes should be expected.
There will be no support for older API versions until version 1.0.x is reached (currently 0.0.x)

## Implementation

## Webhook Management

| Endpoint / Event | API | Implementation |    |
|------------------|-----|----------------|----|
| List Webhooks    | ✅   | Implemented    | ✅  |
| Create Webhook   | ✅   | Implemented    | ✅  |
| Update Webook    | ✅   | Implemented    | ✅  |
| Delete Webook    | ✅   | Implemented    | ✅  |


## Invoices

| Endpoint / Event | API | Implementation                                                                      |    |
|------------------|---|-------------------------------------------------------------------------------------|----|
| Create Invoice   | ✅ | Partially Implemented (payment URL is valid but the UI is not implemented)          | ✅  |
| Get Invoice      | ✅ | Implemented. An invoiced created using the Create Invoice endpoint can be retrieved | ✅  |
| invoice.created  | ✅ | Implemented. Sent on successful call to Create Invoice                              | ✅  |
| invoice.update   | ✅ | Not Implemented                                                                     | ❌  |       

## Trust Deposits

| Endpoint / Event     | API | Implementation                                                                     |   |
|----------------------|---|------------------------------------------------------------------------------------|---|
| Create Trust Deposit | ✅ | Partially Implemented (payment URL is valid but the UI is not implemented)         | ✅ |
| Get Trust Deposit    | ✅ | Implemented. An invoiced created using the Trust Deposit endpoint can be retrieved | ✅ |
| invoice.created      | ✅ | Implemented. Sent on successful call to Create Invoice                             | ✅ |
| invoice.update       | ✅ | Not Implemented                                                                    | ❌ |       

## Payouts

| Endpoint / Event | API | Implementation                                        |    |
|------------------|-----|-------------------------------------------------------|----|
| Get Payouts      |  ✅ | Payouts can be searched by filtering on date and firm | ✅  |
| payout.paid      |  ✅ | Implemented                                           | ✅  | 

## Payments

| Endpoint / Event       | API | Status                                                                          |     |
|------------------------|-----|---------------------------------------------------------------------------------|-----|
| Get Payments           | ✅ | Partially implemented - request validation implemented but no results returned. | ❌   |
| Apply External Payment | ✅ | Not implemented -  (allows PMS to record a payment made outside of FeeWise)     | ❌   | 
| payment.received       | ✅ | Not implemented                                                                 | ❌   | 

## Token Management
| Endpoint / Event | API | Status      |    |
|------------------|-----|-------------|----|
| RotateApiKey     | ✅   | Implemented |  ✅ |

## Charges
| Endpoint / Event      | API | Status                                                                          |     |
|-----------------------|-----|---------------------------------------------------------------------------------|-----|
| Get Firm Customers    | ✅ | Partially implemented  | ❌   |
| Create Charge         | ✅ | Partially implemented     | ❌   | 
| Create Charge and Pay | ✅ | Partially implemented   | ❌   | 


## Metadata
| Endpoint / Event         | API | Status                |     |
|--------------------------|-----|-----------------------|-----|
| Add metadata to objects  | ✅ | Not implemented       | ❌   |
| Search object by metdata | ✅ | Not implemented       | ❌   | 



## Roadmap

### Implement External / partial payments

Fully implement including HTTP handlers, database updates, and events

### Implement payments

* Record payments as they come in and send out events. This will activate the payment events and endpoint currently described in the docs
* Implement payment search
* Implement payment list in Invoice

### Implement payouts

* Record payouts as they are made and send out events. This will activate the payout events and endpoint currently described in the docs
* Payout search result pagination.

### Spec and client libraries

On first *release* of the spec, a FeeWise github repo, to provide api customers with client code from FeeWise, will be made public. This will contain 
any client code generated by FeeWise. Initially this will be C# but may also include Javascript 



