[ Overview](./README.md)

![plot](./images/linkedin.png)

# Authentication
Currently, our APIs are available to be consumed only by our approved partners. 

FeeWise will provide you with the keys and secrets (api-key and signature key) that you will allow the use of our api.

### Keys provided to partners

### X-CHANNEL-PARTNER-ID
The channel partner ID is

* provided during on-boarding .
* a unique identifier for the partner.
* a required header for all requests.

<br />

---
<br />

### X-API-KEY
The X-API-KEY key is...

* provided during on-boarding.
* a required header for all requests.
* able to be rotated by using the `/rotate-key` endpoint `TODO`

nb: The system will support 2 versions of the X-API-KEY

* Once the X-API-KEY is rotated by the partner, the `previous` X-API-KEY will be supported for
  48 hours, after which, a warning email will be sent to the partners email address.
  A header, X-API-KEY-WARNING will be added to all requests that are sent with the `previous` key.

<br />

---
<br />

### X-FEEWISE-SIGNATURE
The X-FEEWISE-SIGNATURE key is...

* provided during on-boarding to FeeWise.
* `never` sent across the wire, [more detail here](HMAC.md)
* used by FeeWise to sign api responses. [more detail here](./AUTHENTICATION.md)

<br />

---
<br />

## TODO - Sample Request

## TODO - Sample Response
