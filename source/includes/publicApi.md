# Public API (Custom Client)

This section describes the public survey flow for building your own custom client (web, mobile, kiosk, or backend integration).

Public endpoints do not require OAuth token.  
Base path: `/api/v1`

## Step 1. Load public survey base

Use company and survey URL names to load public survey configuration before starting the answer flow.

```http
GET /api/v1/surveys/acme/customer-satisfaction HTTP/1.1
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
  "_id": "66f7d9db2a1f66d5c3f5e901",
  "urlName": "customer-satisfaction",
  "name": { "en": "Customer Satisfaction Survey" },
  "description": { "en": "Please share your feedback" },
  "defaultLanguage": "en",
  "translation": { "en": true, "de": true },
  "disableTrackingLocation": false,
  "cookiesCheck": true,
  "surveyTheme": { "_id": "66f7d9db2a1f66d5c3f5e777" },
  "metaVariablesList": ["userId", "campaignId"],
  "globalMeta": ["userId", "campaignId", "source"]
}
```

### HTTP Request
`GET /api/v1/surveys/:companyUrlName/:surveyUrlName`

### Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
companyUrlName | string | Company URL slug. | Yes |
surveyUrlName | string | Survey URL slug. | Yes |

### Notes
- Returns `404` if company or survey does not exist.
- If survey is outside active dates, response can still return survey object with `message` explaining availability status.

## Step 2. Initialize (or restore) survey answer session

Create or load current survey-answer session.  
This call is required before requesting current step.

```http
POST /api/v1/survey-answers HTTP/1.1
Content-Type: application/json
Host: https://go.screver.com
```

```json
{
  "surveyId": "66f7d9db2a1f66d5c3f5e901",
  "referrer": "https://your-client.example/start",
  "lang": "en",
  "meta": {
    "userId": "u-123",
    "campaignId": "spring-2026"
  },
  "executeMetaQuery": true,
  "assets": ["66f7da832a1f66d5c3f5ea10"]
}
```

> The above request returns the following response:

```http
HTTP/1.1 200 OK
Content-Type: application/json
x-public-sign: eyJhbGciOi...
```

```json
{
  "_id": "66f7db5d2a1f66d5c3f5ec42",
  "surveyId": "66f7d9db2a1f66d5c3f5e901",
  "completed": false
}
```

### HTTP Request
`POST /api/v1/survey-answers`

### Body Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
surveyId | string (ObjectId) | Survey ID. Required when `token` is not provided. | Conditionally |
token | string | Token for private survey flow. | Conditionally |
referrer | string | Referrer URL of embedding page/client. | No |
assets | string or array | Asset ID or list of asset IDs. | No |
lang | string | Language key from supported localization list. | No |
meta | object | Custom metadata linked with survey result. | No |
executeMetaQuery | boolean | Enables backend meta processing logic. | No |
reloadResult | boolean | Force result reload behavior. | No |
targetId | string | Optional target identifier. | No |
answer | object | Optional predefined answer map by survey item ID. | No |

### Notes
- Save `x-public-sign` header and send it in next API calls as `publicSign` parameter.
- Your client can safely call this endpoint multiple times to restore existing progress.

## Step 3. Load current survey step

Request current survey structure (section, items, status) for rendering in your client.

```http
GET /api/v1/survey-answers?surveyId=66f7d9db2a1f66d5c3f5e901&lang=en&publicSign=eyJhbGciOi... HTTP/1.1
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
  "survey": {
    "_id": "66f7d9db2a1f66d5c3f5e901",
    "surveySection": {
      "_id": "66f7dc392a1f66d5c3f5ed11",
      "surveyItems": []
    }
  },
  "statusBarData": {
    "currentStep": 1,
    "totalSteps": 4
  },
  "message": null,
  "answer": {},
  "allowReAnswer": false,
  "isPreview": false,
  "html": null,
  "completed": false
}
```

### HTTP Request
`GET /api/v1/survey-answers`

### Query Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
surveyId | string (ObjectId) | Survey ID. Required when `token` is not provided. | Conditionally |
token | string | Token for private flow. | Conditionally |
publicSign | string | Public sign from init response header. | Recommended |
lang | string | Language for rendered labels/content. | No |
meta | object | Metadata object. | No |
executeMetaQuery | boolean | Enables backend meta processing logic. | No |
deviceId | string | Device ID for loading device-linked session. | No |
assets | string or array | Asset ID(s). | No |

## Step 4. Submit answers

Send answers for current step or for single-question autosave mode.

```http
PUT /api/v1/survey-answers HTTP/1.1
Content-Type: application/json
Host: https://go.screver.com
```

```json
{
  "surveyId": "66f7d9db2a1f66d5c3f5e901",
  "publicSign": "eyJhbGciOi...",
  "lang": "en",
  "changeStep": true,
  "answer": {
    "66f7dd222a1f66d5c3f5ef03": "66f7dd352a1f66d5c3f5ef2b",
    "66f7dd902a1f66d5c3f5ef7f": 8,
    "66f7de0f2a1f66d5c3f5efd1": "yes",
    "66f7de0f2a1f66d5c3f5efd1_customAnswer": "Other custom value"
  },
  "useragent": {
    "isDesktop": true,
    "isMobile": false,
    "isTablet": false
  },
  "meta": {
    "userId": "u-123"
  }
}
```

> The above request returns the following response:

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "survey": {},
  "statusBarData": { "currentStep": 2, "totalSteps": 4 },
  "message": null,
  "quizResult": [],
  "answer": {
    "66f7dd902a1f66d5c3f5ef7f": 8
  },
  "meta": { "userId": "u-123" },
  "completed": false
}
```

### HTTP Request
`PUT /api/v1/survey-answers`

### Body Parameters

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
surveyId | string (ObjectId) | Survey ID. Required when `token` is not provided. | Conditionally |
token | string | Token for private flow. | Conditionally |
publicSign | string | Public sign from init response header. | Recommended |
answer | object | Map by survey item id. Value can be string, number, array, matrix-object items, or `_customAnswer*` fields. | Yes |
changeStep | boolean | `true` to move to next step, `false` or omitted for same-step save. | No |
lang | string | Language key. | No |
meta | object | Metadata object. | No |
executeMetaQuery | boolean | Enables backend meta processing logic. | No |
useragent | object | Optional device flags (`isDesktop`, `isMobile`, `isTablet`). | No |

## Answer object schema by question type

`answer` is always a map where key is `surveyItemId`:

```json
{
  "answer": {
    "<surveyItemId>": "<value>",
    "<surveyItemId>_customAnswer": "optional custom text"
  }
}
```

How to get `surveyItemId`:
- From Screver UI (survey editor).
- From Bearer-protected survey endpoints in this documentation (v2 survey structure block).

### Value format per `question.type`

Question type | `answer[surveyItemId]` format | Example
--------- | ------- | ----------- |
multipleChoice | string (`questionItemId`) | `"66f...itemId"`
dropdown | string (`questionItemId`) | `"66f...itemId"`
imageChoice | string (`questionItemId`) | `"66f...itemId"`
checkboxes | string[] (`questionItemId[]`) | `["66f...a", "66f...b"]`
linearScale | number | `5`
slider | number | `8`
netPromoterScore | number | `10`
ces | number | `4`
csat | number | `3`
thumbs | string | `"yes"` or `"no"`
text | string | `"Free text answer"`
countryList | string (country id) | `"66f...countryId"`
multipleChoiceMatrix | array of objects | `[{"row":"<gridRowId>","column":"<gridColumnId>"}]`
checkboxMatrix | array of objects | `[{"row":"<gridRowId>","column":"<gridColumnId>"},{"row":"<gridRowId2>","column":"<gridColumnId2>"}]`
multipleScale | array of objects | `[{"questionItem":"<questionItemId>","value":3}]`
order | array of objects | `[{"questionItem":"<questionItemId>","value":1},{"questionItem":"<questionItemId2>","value":2}]`

### Custom answer field

For question types with an "Other / custom" option, send an additional key:

```json
{
  "answer": {
    "66f7dd222a1f66d5c3f5ef03": "66f7dd352a1f66d5c3f5ef2b",
    "66f7dd222a1f66d5c3f5ef03_customAnswer": "My custom option"
  }
}
```

### Exact answer examples by type

```json
{
  "answer": {
    "surveyItemId_multipleChoice": "questionItemId",
    "surveyItemId_dropdown": "questionItemId",
    "surveyItemId_imageChoice": "questionItemId",
    "surveyItemId_checkboxes": ["questionItemId_1", "questionItemId_2"],
    "surveyItemId_linearScale": 7,
    "surveyItemId_slider": 4,
    "surveyItemId_netPromoterScore": 10,
    "surveyItemId_ces": 5,
    "surveyItemId_csat": 4,
    "surveyItemId_thumbs": "yes",
    "surveyItemId_text": "Some free text",
    "surveyItemId_countryList": "countryId",
    "surveyItemId_multipleChoiceMatrix": [{ "row": "gridRowId_1", "column": "gridColumnId_2" }],
    "surveyItemId_checkboxMatrix": [
      { "row": "gridRowId_1", "column": "gridColumnId_2" },
      { "row": "gridRowId_2", "column": "gridColumnId_1" }
    ],
    "surveyItemId_multipleScale": [
      { "questionItem": "questionItemId_1", "value": 3 },
      { "questionItem": "questionItemId_2", "value": 5 }
    ],
    "surveyItemId_order": [
      { "questionItem": "questionItemId_1", "value": 1 },
      { "questionItem": "questionItemId_2", "value": 2 }
    ],
    "surveyItemId_multipleChoice_customAnswer": "Custom option text"
  }
}
```

### `publicSign` contract

- On init (`POST /api/v1/survey-answers`) backend can return `x-public-sign` response header.
- Save this value in your client state.
- Send it in next requests as `publicSign`:
  - `GET` endpoints: in query.
  - `PUT/POST` endpoints: in body.
- Recommended for iframe/public custom client integrations.

### `changeStep` behavior

- `changeStep: false` (or omitted): save answer on current step.
- `changeStep: true`: run step validation and move to next step.
- Required answers are enforced when moving step (`changeStep: true`).

### Step constraints

You can submit only `surveyItemId` values that belong to the current step returned by `GET /api/v1/survey-answers`.  
If payload includes items from another step, backend returns `422 Unprocessable Entity`.

### Validation error examples

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json
```

```json
{
  "message": {
    "66f7dd902a1f66d5c3f5ef7f": "This field is required"
  }
}
```

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json
```

```json
{
  "message": "Your request contain item that is not allowed on this survey step, please refresh page or contact support"
}
```

### Text/date input notes

- `text` + `input=email`: must be a valid email.
- `text` + `input=number`: must be numeric (float/integer accepted by backend validation).
- `text` + `input=date`: value is a string, format depends on `question.dateParams.type`:
  - `date`: `YYYY-MM-DD`
  - `dateAndTime`: `YYYY-MM-DD-HH:mm`
  - `range`: `YYYY-MM-DD-YYYY-MM-DD`
  - `rangeAndTime`: `YYYY-MM-DD-HH:mm-YYYY-MM-DD-HH:mm`

### Minimal end-to-end flow

1. `GET /api/v1/surveys/:companyUrlName/:surveyUrlName`
2. `POST /api/v1/survey-answers` (save `x-public-sign`)
3. `GET /api/v1/survey-answers` (render current step)
4. `PUT /api/v1/survey-answers` (`changeStep=true` to move next)
5. Repeat steps 3-4 until `completed=true`
6. Optional: `GET /api/v1/survey-answers/result`

## Step 5. Step navigation

### 5.1 Go one step back

```http
GET /api/v1/survey-answers/step-back?surveyId=66f7d9db2a1f66d5c3f5e901&lang=en&publicSign=eyJhbGciOi... HTTP/1.1
Content-Type: application/json
Host: https://go.screver.com
```

### HTTP Request
`GET /api/v1/survey-answers/step-back`

### 5.2 Restart survey

```http
GET /api/v1/survey-answers/restart-survey?surveyId=66f7d9db2a1f66d5c3f5e901&lang=en&dropAnswers=true&publicSign=eyJhbGciOi... HTTP/1.1
Content-Type: application/json
Host: https://go.screver.com
```

### HTTP Request
`GET /api/v1/survey-answers/restart-survey`

### Query Parameters (both endpoints)

Parameter | Type | Description | Required |
--------- | ------- | ----------- | -------- |
surveyId | string (ObjectId) | Survey ID. Required when `token` is not provided. | Conditionally |
token | string | Token for private flow. | Conditionally |
publicSign | string | Public sign from init response header. | Recommended |
lang | string | Language key. | No |
meta | object | Metadata object. | No |
dropAnswers | boolean | Restart endpoint only. Drops existing answers. | No |

## Step 6. Optional utility endpoints

### Save device data
`POST /api/v1/survey-answers/set-device`

Request body example:

```json
{
  "surveyId": "66f7d9db2a1f66d5c3f5e901",
  "deviceId": "device-abc-123",
  "deviceData": {
    "height": "812px"
  }
}
```

### Get answer result
`GET /api/v1/survey-answers/result`

Typical query:

```http
GET /api/v1/survey-answers/result?surveyId=66f7d9db2a1f66d5c3f5e901&publicSign=eyJhbGciOi... HTTP/1.1
Host: https://go.screver.com
```

## Error handling recommendations

- `400` for request validation errors (Joi validation).
- `422` for step/item consistency errors (answering items outside current step).
- `404` for missing company/survey/resources.
- API may return business-level `message` in successful status when survey is unavailable by date or business rules.
- Always handle both HTTP status and response payload (`message`, validation error map) in your custom client.

## Troubleshooting

- `404` on base survey endpoint: verify `companyUrlName` and `surveyUrlName`.
- `400` on update: check `answer` value format for the specific `question.type`.
- `422` on update: ensure submitted `surveyItemId` belongs to current step.
- Survey not available but request is successful: check response `message` (date/business rule restriction).
