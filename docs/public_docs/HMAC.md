[ Overview](./README.md)

![plot](./images/linkedin.png)

# FeeWise api request / response signature(s)

#### Best Practices
Partners should always verify that responses (or Webhook events) are sent from FeeWise by verifying the message signatures.

#### FeeWise message integrity and authenticity:
FeeWise will use HMAC to sign responses (and webhook events it sends to your endpoints) by including a signature in each response header (details of the header below).
The HMAC signature allows clients to verify that the responses / events were sent by FeeWise, not by a third party.
You can verify FeeWiseHMAC signatures by using the details below.

HMACs provide a fast way to tokenize or sign data such as web API requests, credit cards, bank routing information, or personally identifiable information (PII)

HMACs offer two distinct benefits:

* `Message integrity`: As with all hash functions, the output of an HMAC will result in precisely one unique digest of the message’s content.
  If there is any change to the data object (for example modification of an invoice by a single digit: from $100 to $1000), then verification of the original digest will fail.


* `Message authenticity`: What distinguishes HMAC from other hash methods is the use of a secret key to provide message authenticity.
  Only message hashes that were created with the partners FeeWise signing key will produce the same HMAC output.
  Since the signing key is never sent across the wire, this ensures that no third party can substitute their own message content and create a valid HMAC without the intended verifier detecting the change.

---

##### Signing Secret
Before you can verify signatures, you need to retrieve your signing secret. nb: initially, this signing key exchange will likely be done manually, [see here](./AUTHENTICATION.md) for more details.) 

#### Notes
* The api will sign all partner responses with the partner's signature key.
* The api will sign all partner webhook events with the partner's signature key.

---

### Preventing replay attacks
Replay attacks occur when attackers intercept valid payloads and signatures and re-transmit them.

To mitigate such attacks, FeeWise includes a timestamp in the FeeWise signature header.

Because this timestamp is part of the signed payload, it is also verified by the signature, so an attacker cannot change the timestamp without invalidating the signature. If the signature is valid but the timestamp is too old, you can have your application reject the payload.

FeeWise generates the timestamp and signature each time we send an event to your endpoint. If FeeWise retries an event (for example, your endpoint previously replied with a non-2xx status code), then we generate a new signature and timestamp for the new delivery attempt.

---

## TODO rewrite from client perspective

### Verification Steps
#### Step 1: Extract the timestamp and signatures from the header
TODO - decide upon signature format

#### Step 2: Prepare the `signed_request_body` string
Create the `signed_request_body` string by concatenating:

* The current timestamp (as unix timestamp)
* The character `.`
* The actual payload (that is, the request body)

#### Step 3: Determine the expected signature
Compute an HMAC with the SHA256 hash function.
Use the signing secret as the key, and use the `signed_request_body` string as the message.

#### Step 4: Compare the signatures
Compare the signature (or signatures) in the header to the expected signature. For an equality match, compute the difference between the current timestamp and the received timestamp, then decide if the difference is within your time tolerance.
To protect against timing attacks, use a constant-time string comparison to compare the expected signature to each of the received signatures.

For webhook events, if the signature is invalid, reject it with a 401 status code.
