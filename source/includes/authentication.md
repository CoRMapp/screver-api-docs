# Authentication

> To get an access token, send the following request:

```shell
curl --insecure --user 'clientid:clientsecret' 'https://go.screver.com/oauth/token' --data 'grant_type=client_credentials'
```

> Make sure to replace `clientid` and `clientsecret` with your OAuth client id and secret.

> The above command returns structure like this:

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

To allow access to the API use access token.
An OAuth client credentials request is used to obtain a token.
To get your OAuth `client id` and `client secret` please contact us.
The token can be used 24h.

`Authorization: Bearer u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3`

<aside class="notice">
You must replace <code>u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3</code> with the access token you received from the OAuth request.
</aside>
