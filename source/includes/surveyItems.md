# Survey Items

`Survey Item` - specific part of survey. It could contain question or HTML content.

If `surveyItem` contain question, it keep question logic and configurations like:
custom labels, is question required, min/max answers and others.

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

### HTTP Request
`GET /api/v2/survey-items/:id`

### Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
id |string| Id of specific survey item.| Yes |

## Generate answers links

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

### HTTP Request
`POST /api/v2/survey-items/:id/generate-links`

Generate specific links from answering to smiley-type question from email.
After sending array of invitations, system would create invite by each email and return generated links
by answering from email.

Each link include:

`token` - unique invite token,

`surveyItem` - id of entity related with question, use from answering

`value` - answer value by each smiley

### Body

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
invitations |array| Array of invitation objects. Object keys - `email`: user email (string, required), `ttl`: token time-to-live in ms, override global ttl (number, not required), `meta`: invitation object meta data to make search or delete results, example - `meta: { userId: 'userId', day: '01.01.2020' }` (object, not required) | Yes |
ttl |number| Token time-to-live in ms.| No |
