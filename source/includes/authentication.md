# Authentication (Bearer Token)

Use Bearer authentication for protected endpoints (primarily `/api/v2/*`).

Public runtime endpoints (`/api/v1/surveys/...`, `/api/v1/survey-answers...`) do not require Bearer token by default.

## 1. Request access token

```http
POST /oauth/token HTTP/1.1
Host: https://go.screver.com
Authorization: Basic <base64(clientid:clientsecret)>
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials
```

> The above request returns:

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "token_type": "Bearer",
  "access_token": "u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3"
}
```

To get your OAuth `client id` and `client secret`, contact the Screver team.

Token lifetime is 24 hours.

## 2. Use token in API requests

```http
GET /api/v2/surveys?limit=5 HTTP/1.1
Authorization: Bearer u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3
Content-Type: application/json
Host: https://go.screver.com
```

<aside class="notice">
You must replace <code>u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3</code> with the access token you received from the OAuth request.
</aside>
