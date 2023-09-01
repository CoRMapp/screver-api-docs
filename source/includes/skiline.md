# Skiline integration

Data exchange between system provided by metadata params and widget callback.

Callback would send back all result related data on each survey state changes.

Webhook would send all data to endpoint, once survey is completed.

## Connect widget callback

Instructions how to implement a callback mechanism in a JavaScript web application
that communicates with both `Android` and `iOS` platforms through WebView.

We have implemented a feature that allows our JavaScript web application to communicate with native `Android` and `iOS`
components using WebView.
This feature enables seamless data exchange and interaction between the web app and the mobile platforms.

Here's a step-by-step guide to implementing this feature:

`1. *** Android Integration ***:`

- In `Android WebView`, enable JavaScript and set up a JavaScript interface that will serve as a bridge between the
  WebView and native Android code.

- When developing a web application that's designed specifically for the WebView in your Android app, you can create
  interfaces between your JavaScript code and client-side Android code.
  Our `Front-end part(JavaScript code)` can call a method in your Android code to send data to your app
  For example, you can include the following class in your Android app:

<code>
    class WebAppInterface(private val mContext: Context) { <br/>
        /** reveice data from Screver app  **/ <br/>
        fun onDataReceived(data) { ... } <br/>
    }
</code>

In this example, the `WebAppInterface` class allows the web page to send data, using the `onDataReceived()` method.

You can bind this class to the JavaScript that runs in your WebView with `addJavascriptInterface()` and name the
interface `Android`. For example:

`webView.addJavascriptInterface(WebAppInterface(this), "Android")`

On our side we'll use function:

`Android.onDataReceived(dataToSend)`

`2. *** iOS Integration ***:`

- In `iOS WebView`, configure the WebView to handle JavaScript messages using the `WKScriptMessageHandler` protocol.

- Implement the `userContentController(_:didReceive:)` function in your iOS code to receive and process the JavaScript
  message.
  Add a script message handler to receive messages from the web app:

   ```
    configuration.userContentController.add(self, name: "callbackHandler")
   ```

On our side we'll use function:

`window.webkit.messageHandlers.callbackHandler.postMessage(dataToSend)`

**Response**

``` json
{
 "completed":false,
 "statusBarData": {
  "passed":0,
  "passedSection":0,
  "total":3,
  "totalSection":3
 },
 "survey": {
  "id": "64e752ca97a1131105c9c62a",
  "name": "Survey name"
 },
 "meta": {
  "name": "User Name"
 },
 "answer":{
  "64ac09a858298c30bb797e5a": {
    "value": 1
  }
 },
 "height":"205px",
}
```

 Parameter     | Type   | Description                        |
---------------|--------|------------------------------------|
 completed     | bool   | Survey passed                      |
 height        | string | height of Screver widget           |
 answer        | object | answers data                       |
 survey        | object | id - survey id, name - survey name |
 statusBarData | object | survey progress data               |
 meta          | object | meta params                        |

## Meta data object

Meta data - data could be passed on creation of result, data would be returned back on widget callback or webhook.

Could contain any useful information like userId, timestamp, eventType, etc. - can be used later to aggregate survey
results.

Format: URL query object

Example query:

`?meta.userId=123&meta.timestamp=1692872269&meta.eventType=first_visit`

### Meta data access control

It is possible to restrict access to survey by meta.

In survey settings "Meta control" tab, you could define meta access key, if activated, then only possible to answer
survey, if present `meta.accessKey`

Example query:

`?meta.accessKey=123123`

Only results with correct `meta.accessKey` would init, rest - raise error.

### Meta variables whitelist

You can define whitelist of meta-variables, to be used in survey answering form.
Only whitelisted variables would be processed.

Config - survey settings "Meta control" tab.
Each key would have value (fallback), in case if value would be not mapped from URL params

Example whitelist:

`{ firstName: 'User', service: 'provider' }`

Example query:

`?meta.firstName=John&meta.service=Alturos`

In result, you can define question like:

`Hi ${firstName}, please rate our ${service}`,

variables data would be taken from URL meta params

## Survey query params

Survey query params - query params that could modify answering flow for the end user.

### Switch language

Query param - "lang", could override default survey language for the end user, but only if survey have translation for
provided language.

Value - locale shortcode.

Example: `?lang=de`

### Force reload result

If survey have enabled config "allowReload" activated,
then it is possible to start new result from same device by pass URL param: "reloadResult"

Example: `?reloadResult=true`

Then new result would be created for the same device, old result would be still keeped in system, but not possible to
answer.
On success initialization - param would be removed from ULR by system.

## API: Get list of results by meta

Return list of results by meta query, useful to understand if user had already passed survey, or build custom widget
depended on answer results.

```http
POST /api/v1/survey-results/by-meta HTTP/1.1
Content-Type: application/json
Host: https://go.screver.com
```

```json
{
  "companyId": "64e72bac2475473a59e4ba95",
  "meta": {
    "userId": "111",
    "eventType": "first_visit"
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
  "resources": [
    {
      "_id": "64ef5448afff7fc7c3c7d791",
      "completed": false,
      "survey": {
        "_id": "64ef5448afff7fc7c3c7d752",
        "name": {
          "en": "restaurant visit feedback"
        },
        "overallScore": 100
      },
      "meta": {
        "userId": "111",
        "eventType": "first_visit",
        "campaign": "restaurant"
      },
      "answer": {
        "64ef5448afff7fc7c3c7d789": {
          "value": 2
        }
      },
      "createdAt": "2023-08-30T14:38:00.898Z",
      "scorePoints": 20
    },
    {
      "_id": "64ef5448afff7fc7c3c7d790",
      "completed": false,
      "survey": {
        "_id": "64ef5448afff7fc7c3c7d752",
        "name": {
          "en": "restaurant visit feedback"
        },
        "overallScore": 100
      },
      "meta": {
        "userId": "111",
        "eventType": "first_visit",
        "campaign": "restaurant"
      },
      "answer": {
        "64ef5448afff7fc7c3c7d78b": {
          "value": 10
        }
      },
      "createdAt": "2023-08-30T14:38:00.892Z",
      "scorePoints": 10
    }
  ],
  "total": 2
}
```

### HTTP Request

`POST /api/v1/survey-results/by-meta`

### Body

 Parameter | Type   | Description                                                                                     | Valid            | Required 
-----------|--------|-------------------------------------------------------------------------------------------------|------------------|----------|
 companyId | string | Screver Company ID.                                                                             | any              | Yes      |
 meta      | object | Meta object - linked to results data. Example meta: { userId: '123', eventType: 'first_visit' } | obj min keys: 1  | Yes      |
 surveyId  | string | Filter results by surveyId                                                                      | any              | No       |
 skip      | number | Count of skipped items for pagination.                                                          | any              | No       |
 limit     | number | Count of returned items in response. Default: 50                                                | `5`, `50`, `100` | No       |
 from      | date   | Filtering results by date "from". Example: { from: '2023-08-29T14:58:26.179Z' }                 | any              | No       |
 to        | date   | Filtering results by date "to". Example: { to: '2023-08-31T14:58:26.180Z' }                     | any              | No       |
