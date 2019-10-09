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

### HTTP Request
`GET /api/v2/surveys`

### Query Parameters

Parameter | Type | Description | Valid  | Required
--------- | ------- | ------------ | ------- | ----- |
skip |number| Count of skipped items for pagination.| any | No |
limit|number| Count of returned items in response.| `5`, `10`, `25`, `50`, `100` | Yes |
sort|string| Sort object, with single key: key - sort field, value - order (`1` - `ASC`, `-1` - `DESC`). Example: `{ createdAt: -1 }` |`createdAt`, `updatedAt`, `name`| No|

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

### HTTP Request
`GET /api/v2/surveys/:id`

### Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
id |string| Id of specific survey.| Yes |
