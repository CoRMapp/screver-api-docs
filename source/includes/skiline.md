# Skiline integration
TBD

## Connect widget callback
Instructions how to implement a callback mechanism in a JavaScript web application
that communicates with both `Android` and `iOS` platforms through WebView.

We have implemented a feature that allows our JavaScript web application to communicate with native `Android` and `iOS` components using WebView.
This feature enables seamless data exchange and interaction between the web app and the mobile platforms.

Here's a step-by-step guide to implementing this feature:

`1. *** Android Integration ***:`

- In `Android WebView`, enable JavaScript and set up a JavaScript interface that will serve as a bridge between the WebView and native Android code.

- When developing a web application that's designed specifically for the WebView in your Android app, you can create interfaces between your JavaScript code and client-side Android code.
  Our `Front-end part(JavaScript code)` can call a method in your Android code to send data to your app
  For example, you can include the following class in your Android app:
  
<code>
    class WebAppInterface(private val mContext: Context) { <br/>
        /** reveice data from Screver app  **/ <br/>
        fun onDataReceived(data) { ... } <br/>
    }
</code>
   
   In this example, the `WebAppInterface` class allows the web page to send data, using the `onDataReceived()` method.
   
   You can bind this class to the JavaScript that runs in your WebView with `addJavascriptInterface()` and name the interface `Android`. For example:
   
 `webView.addJavascriptInterface(WebAppInterface(this), "Android")`
  
  On our side we'll use function:
  
   `Android.onDataReceived(dataToSend)`
  

`2. *** iOS Integration ***:`

   - In `iOS WebView`, configure the WebView to handle JavaScript messages using the `WKScriptMessageHandler` protocol.
   
   - Implement the `userContentController(_:didReceive:)` function in your iOS code to receive and process the JavaScript message.
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

Parameter | Type | Description |
--------- | ------- | ----------- |
completed |bool| Survey passed |
height |string| height of Screver widget |
answer |object| answers data |
survey |object| id - survey id, name - survey name |
statusBarData |object| survey progress data |
meta |object| meta params |


## Meta data
