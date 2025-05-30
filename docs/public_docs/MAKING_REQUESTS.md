[ Overview](./README.md)

![plot](./images/linkedin.png)

# Making Requests

All requests to the API require a valid channel partner ID and api-key issued by FeeWise (see [Authentication](./AUTHENTICATION.md)).

TODO - HMAC Header in response

### Example Request

```bash
curl --location --request GET 'http://localhost:8080/api/v3/partner/events/types' \
--header 'Accept: application/json' \
--header 'X-Channel-Partner-ID: 3ce8fa13-ca7a-4e73-a6df-e7ed70515ed8' \
--header 'X-API-KEY: 27ab4b89-5951-4293-a793-fe64c51e5b6c' \
--header 'X-Correlation-ID: deadbeef-0000-4000-a000-000000facade'
```

### Example Response
```bash
{
    "events": [
        "artifact.invoice.created",
        "artifact.invoice.created",
        "webhook.created",
        "webhook.deleted",
        "webhook.failed",
        "webhook.sent",
    ]
}
```

### Raw Log
```bash
GET /api/v3/partner/events/types HTTP/1.1
Accept: application/json
X-Channel-Partner-ID: 5ca1ab1e-cafe-4000-a000-deadbeefdead
X-API-KEY: decade00-0000-4000-a000-000000facade
X-Correlation-ID: deadbeef-0000-4000-a000-000000facade
User-Agent: Dredd-I-am-the-Law/1.5
Cache-Control: no-cache
Host: localhost:8080
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
 
HTTP/1.1 200 OK
Content-Type: application/json
Date: Wed, 27 Jul 2022 23:59:23 GMT
Content-Length: 230
 
{
"events": [
"artifact.invoice.created",
"artifact.invoice.created",
"webhook.created",
"webhook.deleted",
"webhook.failed",
"webhook.sent",
]
}
```

### Tracking requests
A Correlation ID is a unique identifier value attached to requests and messages allowing reference to a particular transaction or event chain.
FeeWise accepts an X-Correlation-ID header in http requests. A correlation ID header will always be provided in the response header. See [Webhooks](./WEBHOOKS.md) for more information.
