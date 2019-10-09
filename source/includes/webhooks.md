# Webhooks

You can configure webhook endpoints via the API to be notified about events that happen.

`POST` payloads that are delivered to your webhook's configured URL endpoint will contain special header:

`X-API-SIGNATURE` - The HMAC hex digest of the response body. Each webhook have own generated `secret`.
The HMAC hex digest is generated using the `sha256` hash function and the secret as the HMAC `key`.


Webhook endpoint must have a url and type.
Type is related to webhook event.

Valid types:

`optionSelected` - Event fired when user click on predefined answer in email.

Response fields:

Name | Type | Description |
--------- | ------- | ----------- |
timestamp |string| Time when event fired.|
surveyItemId |string| Id of survey item, that contain question.|
meta |object| Result meta object from invitation.|
question |object| Question object.|
answer |object| Answer value (id or number).|

`surveyCompleted` - Event fired when user complete survey.

Response fields:

Name | Type | Description |
--------- | ------- | ----------- |
timestamp |string| Time when event fired.|
meta |object| Result meta object from invitation.|

`*` - Wildcard event, set this if you want to receive all events to one endpoint.



## Create webhook

```http
POST /api/v2/webhooks HTTP/1.1
Authorization: Bearer u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3
Content-Type: application/json
Host: https://go.screver.com
```

```json
{
 "type": "optionSelected",
 "url": "https://go.screver.com/api/v1/test-webhook"
}
```

> The above request returns the following response:

```http
HTTP/1.1 201 Created
```

```json
{
    "_id": "5d9b4816de62163caf637d5c",
    "type": "optionSelected",
    "company": "5d00f1e3001530581cc1ea85",
    "url": "https://go.screver.com/api/v1/test-webhook",
    "secret": "f6353acf-bca0-4992-8313-0d509f80c4f1",
    "createdAt": "2019-10-07T14:13:42.489Z",
    "updatedAt": "2019-10-07T14:13:42.489Z",
    "__v": 0
}
```

### HTTP Request
`POST /api/v2/webhooks`

### Body

Parameter | Type | Description | Valid | Required |
--------- | ------- | ----------- | ------ | -------- |
type |string| Webhook type.| `optionSelected`, `surveyCompleted`, `*` | No |
url |string| Webhook callback url.| any | No |



## Update webhook by id

```http
PUT /api/v2/webhooks/5d9b4816de62163caf637d5c HTTP/1.1
Authorization: Bearer u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3
Content-Type: application/json
Host: https://go.screver.com
```

```json
{
 "type": "optionSelected",
 "url": "https://go.screver.com/api/v1/test-webhook"
}
```

> The above request returns the following response:

```http
HTTP/1.1 200 OK
```

```json
{
    "type": "optionSelected",
    "_id": "5d9b4816de62163caf637d5c",
    "url": "https://go.screver.com/api/v1/test-webhook",
    "secret": "f6353acf-bca0-4992-8313-0d509f80c4f1",
    "createdAt": "2019-10-07T14:13:42.489Z",
    "updatedAt": "2019-10-07T14:30:05.313Z"
}
```

### HTTP Request
`PUT /api/v2/webhooks/:id`

### Body

Parameter | Type | Description | Valid | Required |
--------- | ------- | ----------- | ------ | -------- |
type |string| Webhook type.| `optionSelected`, `surveyCompleted`, `*` | No |
url |string| Webhook callback url.| any | No |



## Get list of webhooks with base data.

```http
GET /api/v2/webhooks?limit=5 HTTP/1.1
Authorization: Bearer u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3
Content-Type: application/json
Host: https://go.screver.com
```

> The above request returns the following response:

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
    "resources": [
        {
            "_id": "5d9c378127a91314f83f9802",
            "type": "surveyCompleted",
            "url": "https://go.screver.com/api/v1/test-webhook2",
            "secret": "09e90103-3dc9-4378-9402-c58e87d38ddd",
            "createdAt": "2019-10-08T07:15:13.945Z",
            "updatedAt": "2019-10-08T07:15:13.945Z"
        },
        {
            "_id": "5d9c377c27a91314f83f9801",
            "type": "optionSelected",
            "url": "https://go.screver.com/api/v1/test-webhook2",
            "secret": "33d30530-fe4b-469e-9e14-e9ef19b9775b",
            "createdAt": "2019-10-08T07:15:08.517Z",
            "updatedAt": "2019-10-08T07:15:08.517Z"
        },
        {
            "_id": "5d9c377227a91314f83f97ff",
            "type": "*",
            "url": "https://go.screver.com/api/v1/test-webhook",
            "secret": "970808e3-52ac-4d8c-b584-5c8123a72698",
            "createdAt": "2019-10-08T07:14:58.136Z",
            "updatedAt": "2019-10-08T07:14:58.136Z"
        },
        {
            "_id": "5d9c376c27a91314f83f97fe",
            "type": "surveyCompleted",
            "url": "https://go.screver.com/api/v1/test-webhook",
            "secret": "b2d2693b-f1ad-44c4-b9b6-0cf3534dd00b",
            "createdAt": "2019-10-08T07:14:52.361Z",
            "updatedAt": "2019-10-08T07:14:52.361Z"
        },
        {
            "_id": "5d9b4b4ede62163caf637d5d",
            "type": "optionSelected",
            "url": "https://go.screver.com/api/v1/test-webhook",
            "secret": "1b629c44-e283-44ef-946c-8bce5f014e88",
            "createdAt": "2019-10-07T14:27:26.908Z",
            "updatedAt": "2019-10-08T07:14:40.734Z"
        }
    ],
    "total": 5
}
```

### HTTP Request
`GET /api/v2/webhooks`

### Query Parameters

Parameter | Type | Description | Valid  | Required
--------- | ------- | ------------ | ------- | ----- |
skip |number| Count of skipped items for pagination.| any | No |
limit|number| Count of returned items in response.| `5`, `10`, `25`, `50`, `100` | Yes |
sort|string| Sort object, with single key: key - sort field, value - order (`1` - `ASC`, `-1` - `DESC`). Example: `{ createdAt: -1 }` |`createdAt`, `updatedAt`| No|



## Get specific webhook by ID with all related data.

```http
GET /api/v2/webhooks/5d0b985960a1da78cf8f4a57 HTTP/1.1
Authorization: Bearer u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3
Content-Type: application/json
Host: https://go.screver.com
```

> The above request returns the following response:

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
    "_id": "5d9b4b4ede62163caf637d5d",
    "type": "optionSelected",
    "url": "https://go.screver.com/api/v1/test-webhook",
    "secret": "1b629c44-e283-44ef-946c-8bce5f014e88",
    "createdAt": "2019-10-07T14:27:26.908Z",
    "updatedAt": "2019-10-07T14:27:26.908Z"
}
```

### HTTP Request
`GET /api/v2/webhooks/:id`

### Query Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
id |string| Id of specific webhook.| Yes |



## Delete webhook by id

```http
DELETE /api/v2/webhooks/5d10840f5b4ca0038509890c HTTP/1.1
Authorization: Bearer u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3
Content-Type: application/json
Host: https://go.screver.com
```

> The above request returns the following response:

```http
HTTP/1.1 204 No content
```

### HTTP Request
`DELETE /api/v2/webhooks/:id`

### Query Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
id |string| Id of specific webhook.| Yes |
