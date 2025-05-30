[ Overview](./README.md)

![plot](./images/linkedin.png)

# API Key Rotation

FeeWise authenticates your API requests using your account’s [API keys](./AUTHENTICATION.md).  If you don’t 
include your key when making an API request, or use an incorrect or outdated one, FeeWise returns a 401 - Unauthorized
If your X-API-KEY is compromised, you need to rotate (`roll`) the key, to block any API requests that may use that key.

To allow this key to be rotated, a 
[key rotation endpoint](../../reference/partner-openapispec.yaml/paths/~1api~1v3~1partner~1rotatekey/post) is available. 
This endpoint will return a new API key but leave the old key valid for a period of time to allow the application(s) 
using the partner API to be updated without downtime due to using an expired key.

NB - calling this endpoint again before the new key has been updated in the calling applications will result in the 
application(s) using an invalid key.

When calling the endpoint, the expiry of the previous key may be supplied. If not supplied, system default of 48 hours
will be used. If your X-API-KEY has been compromised, the timestamp for the expiry should be set to the current time 
(or earlier) so the previous key is invalidated immediately.

Example key rotation. Rotate the keys setting the previous key expiry to 24 hours.
```shell
curl --location --request POST 'https://papi.au.sandbox.getfeewise.com/api/v3/partner/rotatekey' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'X-CHANNEL-PARTNER-ID: b5696fe5-2548-4518-a954-31e3a424c912' \
--header 'X-API-KEY: ebf75b3c-9491-414e-9ff0-332e414c68e4' \
--data-raw '{
  "previous_key_expires_hours": 24
}'
```