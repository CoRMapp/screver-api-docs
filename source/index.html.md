---
title: go.screver.com API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - http

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

search: true
---

# Introduction

This is initial go.screver.com API documentation.

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

# Surveys

## Get list of surveys with base data.

```http
GET /api/v2/surveys?limit=5 HTTP/1.1
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
      "_id": "5d0b985960a1da78cf8f4a57",
      "translation": { "en": true, "de": false, "ru": false, "nl": false },
      "name": { "en": "repellat" },
      "description": { "en": "consequuntur" },
      "urlName": "repellat",
      "startDate": "2019-06-20T14:29:45.524Z",
      "endDate": "2019-06-30T14:29:45.525Z",
      "createdAt": "2019-06-20T14:29:45.538Z",
      "updatedAt": "2019-06-20T14:29:45.538Z"
    },
    {
       "_id": "5d0b9859a1da78cf8f4a58",
       "translation": { "en": true, "de": false, "ru": false, "nl": false },
       "name": { "en": "qwerty" },
       "description": { "en": "sdf32324324" },
       "urlName": "qwerty",
       "startDate": "2019-06-20T14:29:45.524Z",
       "endDate": "2019-06-30T14:29:45.525Z",
       "createdAt": "2019-06-20T14:29:45.538Z",
       "updatedAt": "2019-06-20T14:29:45.538Z"
    },
    {
      "_id": "5d0b985960a1da78cf8f4a59",
      "translation": { "en": true, "de": false, "ru": false, "nl": false },
      "name": { "en": "testname" },
      "description": { "en": "consequuntur324" },
      "urlName": "testname",
      "startDate": "2019-06-20T14:29:45.524Z",
      "endDate": "2019-06-30T14:29:45.525Z",
      "createdAt": "2019-06-20T14:29:45.538Z",
      "updatedAt": "2019-06-20T14:29:45.538Z"
    },
    {
      "_id": "5d0b985960a1da78cf8f4a60",
      "translation": { "en": true, "de": false, "ru": false, "nl": false },
      "name": { "en": "bar" },
      "description": { "en": "bar" },
      "urlName": "bar desc",
      "startDate": "2019-06-20T14:29:45.524Z",
      "endDate": "2019-06-30T14:29:45.525Z",
      "createdAt": "2019-06-20T14:29:45.538Z",
      "updatedAt": "2019-06-20T14:29:45.538Z"
    },
    {
      "_id": "5d0b985960a1da78cf8f4a61",
      "translation": { "en": true, "de": false, "ru": false, "nl": false },
      "name": { "en": "foo" },
      "description": { "en": "foo desc" },
      "urlName": "foo",
      "startDate": "2019-06-20T14:29:45.524Z",
      "endDate": "2019-06-30T14:29:45.525Z",
      "createdAt": "2019-06-20T14:29:45.538Z",
      "updatedAt": "2019-06-20T14:29:45.538Z"
    }
  ],
  "total": 20
}
```

### Query Parameters

Parameter | Type | Description | Default | Required
--------- | ------- | ----------- | ----- | -------- |
skip |number| Count of skipped items for pagination.| 10 | No |
limit|number| Count of returned items in response.| 10 | Yes |
sort|string| Sort parameter - name, createdAt, updatedAt | createdAt | No|

## Get specific survey by ID with all related data.

```http
GET /api/v2/surveys/5d0b985960a1da78cf8f4a57 HTTP/1.1
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
  "_id": "5d0b985960a1da78cf8f4a57",
  "translation": { "en": true, "de": false, "ru": false, "nl": false },
  "name": { "en": "repellat" },
  "description": { "en": "consequuntur" },
  "urlName": "repellat",
  "startDate": "2019-06-20T14:29:45.524Z",
  "endDate": "2019-06-30T14:29:45.525Z",
  "createdAt": "2019-06-20T14:29:45.538Z",
  "updatedAt": "2019-06-20T14:29:45.538Z",
  "surveySections":
    [
      {
        "_id":"5d1086759513bd03ca00a579",
        "name": { "en": "fugiat" },
        "survey": "5d1086759513bd03ca00a578",
        "createdBy": "5d1086759513bd03ca00a575",
        "updatedBy":"5d1086759513bd03ca00a575",
        "surveyItems": [
          {
            "_id": "5d1086759513bd03ca00a57a",
            "type": "question",
            "required": false,
            "survey": "5d1086759513bd03ca00a578",
            "surveySection": "5d1086759513bd03ca00a579",
            "question": {
              "_id": "5d1086759513bd03ca00a57b",
              "translation": { "en": true, "de": false, "ru": false, "nl": false },
              "linearScale": { "from": 1, "to": 5, "icon": "smiley" },
              "type": "linearScale",
              "name": { "en": "cupiditate" },
              "createdBy": "5d1086759513bd03ca00a575",
              "updatedBy": "5d1086759513bd03ca00a575"
            }
          }
        ]
      }
    ]
}
```

### Query Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
id |objectId| ObjectId of specific survey.| Yes |

# Survey Items
## Get specific survey item by ID.

```http
GET /api/v2/survey-items/5d0b985960a1da78cf8f4a57 HTTP/1.1
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
  "_id": "5d1086759513bd03ca00a57a",
  "type": "question",
  "required": false,
  "survey": "5d1086759513bd03ca00a578",
  "surveySection": "5d1086759513bd03ca00a579",
  "question": {
    "_id": "5d1086759513bd03ca00a57b",
    "translation": { "en": true, "de": false, "ru": false, "nl": false },
    "linearScale": { "from": 1, "to": 5, "icon": "smiley" },
    "type": "linearScale",
    "name": { "en": "cupiditate" },
    "createdBy": "5d1086759513bd03ca00a575",
    "updatedBy": "5d1086759513bd03ca00a575"
  }
}
```

### Query Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
id |objectId| ObjectId of specific survey item.| Yes |

## Generate answers links
> Generate specific links from answering to smiley-type question from email.
> After sending array of invitations, system would create invite by each email and return generated links
> by answering from email.
> Each link include:
> - token - unique invite token,
> - surveyItem - id of entity related with question, use from answering
> - value - answer value by each smiley

```http
POST /api/v2/survey-items/5d10840f5b4ca0038509890c/generate-links HTTP/1.1
Authorization: Bearer u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3
Content-Type: application/json
Host: https://go.screver.com
```

```json
{
    "invitations": [
        { email: 'example1@email.com', meta: { userId: 'user1' } },
        { email: 'example2@email.com', meta: { userId: 'user2' } },
        { email: 'example3@email.com', meta: { userId: 'user3' } },
    ],
    "ttl": 86400000
}
```

> The above request returns the following response:

```http
HTTP/1.1 200 OK
```

```json
[ { "email": "example1@email.com",
    "links":
     [ "http://go.screver.com/survey?token=4f207be5-a00b-4493-bb39-873db282c614?surveyItem=5d43dc66faa7521f1730ee7e?value=1",
       "http://go.screver.com/survey?token=4f207be5-a00b-4493-bb39-873db282c614?surveyItem=5d43dc66faa7521f1730ee7e?value=2",
       "http://go.screver.com/survey?token=4f207be5-a00b-4493-bb39-873db282c614?surveyItem=5d43dc66faa7521f1730ee7e?value=3",
       "http://go.screver.com/survey?token=4f207be5-a00b-4493-bb39-873db282c614?surveyItem=5d43dc66faa7521f1730ee7e?value=4",
       "http://go.screver.com/survey?token=4f207be5-a00b-4493-bb39-873db282c614?surveyItem=5d43dc66faa7521f1730ee7e?value=5" ] },
  { "email": "example2@email.com",
    "links":
     [ "http://go.screver.com/survey?token=2b69e181-3a16-415a-94f4-0aaa2544cd2e?surveyItem=5d43dc66faa7521f1730ee7e?value=1",
       "http://go.screver.com/survey?token=2b69e181-3a16-415a-94f4-0aaa2544cd2e?surveyItem=5d43dc66faa7521f1730ee7e?value=2",
       "http://go.screver.com/survey?token=2b69e181-3a16-415a-94f4-0aaa2544cd2e?surveyItem=5d43dc66faa7521f1730ee7e?value=3",
       "http://go.screver.com/survey?token=2b69e181-3a16-415a-94f4-0aaa2544cd2e?surveyItem=5d43dc66faa7521f1730ee7e?value=4",
       "http://go.screver.com/survey?token=2b69e181-3a16-415a-94f4-0aaa2544cd2e?surveyItem=5d43dc66faa7521f1730ee7e?value=5" ] },
  { "email": "example3@email.com",
    "links":
     [ "http://go.screver.com/survey?token=92bf5361-90ae-47f9-bc67-66d0af776f5a?surveyItem=5d43dc66faa7521f1730ee7e?value=1",
       "http://go.screver.com/survey?token=92bf5361-90ae-47f9-bc67-66d0af776f5a?surveyItem=5d43dc66faa7521f1730ee7e?value=2",
       "http://go.screver.com/survey?token=92bf5361-90ae-47f9-bc67-66d0af776f5a?surveyItem=5d43dc66faa7521f1730ee7e?value=3",
       "http://go.screver.com/survey?token=92bf5361-90ae-47f9-bc67-66d0af776f5a?surveyItem=5d43dc66faa7521f1730ee7e?value=4",
       "http://go.screver.com/survey?token=92bf5361-90ae-47f9-bc67-66d0af776f5a?surveyItem=5d43dc66faa7521f1730ee7e?value=5" ] } ]
```

### Query Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
invitations |array| Array of invitation objects. Object keys - "email": user email (string, required), "ttl": token time-to-live in ms, override global ttl (number, not required), "meta": invitation object meta data to make search or delete results, example: "meta": { userId: 'userId', day: '01.01.2020' } (object, not required) | Yes |
ttl |number| Token time-to-live in ms.| No |

# Survey Results
## Delete survey result by id
> Delete survey result by ID

```http
DELETE /api/v2/survey-results/5d10840f5b4ca0038509890c HTTP/1.1
Authorization: Bearer u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3
Content-Type: application/json
Host: https://go.screver.com
```

> The above request returns the following response:

```http
HTTP/1.1 204 No content
```

## Delete survey results by array of ids
> Delete survey results by array of ids

```http
DELETE /api/v2/survey-results/remove-array HTTP/1.1
Authorization: Bearer u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3
Content-Type: application/json
Host: https://go.screver.com
```

```json
{
  "idsArray": [ "5d10840f5b4ca0038509890c", "5d10840f5b4ca0038509465r", "5d10840f5b4ca0038509978x" ]
}
```

> The above request returns the following response:

```http
HTTP/1.1 204 No content
```

### Query Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
idsArray |array| Array of ObjectIds.| Yes |

## Delete survey results by meta
> Delete survey results by meta stored in survey result.

```http
DELETE /api/v2/survey-results/remove-by-meta HTTP/1.1
Authorization: Bearer u8ptxAd2hJ3aRjtgwwmUqqkNpcMOYxf3
Content-Type: application/json
Host: https://go.screver.com
```

```json
{
  "meta": {
    "userId": "123123"
  }
}
```

> The above request returns the following response:

```http
HTTP/1.1 204 No content
```

### Query Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
meta |Object| ObjectId of meta data.| No |

# Webhooks

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

### Query Parameters

Parameter | Type | Description | Default | Required
--------- | ------- | ----------- | ----- | -------- |
skip |number| Count of skipped items for pagination.| 10 | No |
limit|number| Count of returned items in response.| 10 | Yes |
sort|string| Sort parameter - createdAt, updatedAt | createdAt | No|

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
    "url": "https://go.screver.com//api/v1/test-webhook",
    "secret": "1b629c44-e283-44ef-946c-8bce5f014e88",
    "createdAt": "2019-10-07T14:27:26.908Z",
    "updatedAt": "2019-10-07T14:27:26.908Z"
}
```

### Query Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
id |objectId| ObjectId of specific webhook.| Yes |

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

### Body

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
type |string| Webhook type (one of [optionSelected, surveyCompleted, *]).| Yes |
url |string| Webhook callback url.| Yes |

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
    "url": "https://go.screver.com//api/v1/test-webhook",
    "secret": "f6353acf-bca0-4992-8313-0d509f80c4f1",
    "createdAt": "2019-10-07T14:13:42.489Z",
    "updatedAt": "2019-10-07T14:30:05.313Z"
}
```
### Query Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
id |objectId| ObjectId of specific webhook.| Yes |

### Body

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
type |string| Webhook type (one of [optionSelected, surveyCompleted, *]).| No |
url |string| Webhook callback url.| No |

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

### Query Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
id |objectId| ObjectId of specific webhook.| Yes |
