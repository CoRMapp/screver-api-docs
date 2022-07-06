# Tableau Integration

Get survey results data prepared for Tableau inserting.

Have 2 similar endpoints with different authorization process:

`GET /api/v1/tableau/get-data/jwt` - JWT browser authorization for testing via browser

`GET /api/v1/tableau/get-data` - Server-to-Server OAuth Bearer token auth

```http
GET /api/v1/tableau/get-data HTTP/1.1
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
  "data": [
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a9875eb7ba77479ba3872a",
      "questionType": "Image Choice",
      "questionText": "Question 1",
      "optionId": "62a9875eb7ba77479ba3872c",
      "optionName": "Option 2",
      "optionType": "string",
      "value": "",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a98761cb3cda478b55609f",
      "questionType": "Dropdown",
      "questionText": "Question 2",
      "optionId": "62a98774cb3cda478b556310",
      "optionName": "Option 3",
      "optionType": "string",
      "value": "",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a98766cb3cda478b5560ad",
      "questionType": "Text",
      "questionText": "Question 3",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": "aa",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a9876bb7ba77479ba3873f",
      "questionType": "Text",
      "questionText": "Question 4",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": "123",
      "valueNumeric": 123,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a9876fcb3cda478b5562f9",
      "questionType": "Order",
      "questionText": "Question 5",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": 0,
      "valueNumeric": 0,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a9876fcb3cda478b5562f9",
      "questionType": "Order",
      "questionText": "Question 5",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": 1,
      "valueNumeric": 1,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a9876fcb3cda478b5562f9",
      "questionType": "Order",
      "questionText": "Question 5",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": 2,
      "valueNumeric": 2,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a98799b7ba77479ba38772",
      "questionType": "Checkboxes",
      "questionText": "Question 6",
      "optionId": "62a9879db7ba77479ba38789",
      "optionName": "None of the above",
      "optionType": "string",
      "value": "",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a987a1cb3cda478b55633f",
      "questionType": "Checkbox Matrix",
      "questionText": "Question 7",
      "optionId": "62a987a4b7ba77479ba38798-62a987a1cb3cda478b556341",
      "optionName": "Row 2 - Column 1",
      "optionType": "string",
      "value": "",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a987a1cb3cda478b55633f",
      "questionType": "Checkbox Matrix",
      "questionText": "Question 7",
      "optionId": "62a987a1cb3cda478b556340-62a987a6b7ba77479ba387a0",
      "optionName": "Row 1 - Column 2",
      "optionType": "string",
      "value": "",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a987a1cb3cda478b55633f",
      "questionType": "Checkbox Matrix",
      "questionText": "Question 7",
      "optionId": "62a987a5cb3cda478b556355-62a987bccb3cda478b5565dd",
      "optionName": "Row 3 - “I can’t tell”",
      "optionType": "string",
      "value": "",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a987bfb7ba77479ba387b4",
      "questionType": "Multiple Choice",
      "questionText": "Question 8",
      "optionId": "62a987c1cb3cda478b5565e5",
      "optionName": "Option 2",
      "optionType": "string",
      "value": "",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a987c7b7ba77479ba387cb",
      "questionType": "Multiple Choice Matrix",
      "questionText": "Question 9",
      "optionId": "62a987c7b7ba77479ba387cc-62a987cbcb3cda478b5565fa",
      "optionName": "Row 1 - Column 2",
      "optionType": "string",
      "value": "",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a987c7b7ba77479ba387cb",
      "questionType": "Multiple Choice Matrix",
      "questionText": "Question 9",
      "optionId": "62a987cbb7ba77479ba387db-62a987d0b7ba77479ba387eb",
      "optionName": "Row 2 - “I can’t tell”",
      "optionType": "string",
      "value": "",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a987d5b7ba77479ba387f3",
      "questionType": "Multiple Scale",
      "questionText": "Question 10",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": 4,
      "valueNumeric": 4,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a987dfb7ba77479ba38807",
      "questionType": "Linear Scale",
      "questionText": "Question 11",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": 4,
      "valueNumeric": 4,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a987e8b7ba77479ba38817",
      "questionType": "Multiple Scale",
      "questionText": "Question 12",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": 9,
      "valueNumeric": 9,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a987f2cb3cda478b55686f",
      "questionType": "Linear Scale",
      "questionText": "Question 13",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": 4,
      "valueNumeric": 4,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a98800b7ba77479ba38849",
      "questionType": "Multiple Scale",
      "questionText": "Question 14",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": 10,
      "valueNumeric": 10,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a9880bcb3cda478b5568a9",
      "questionType": "Multiple Scale",
      "questionText": "Question 15",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": 3,
      "valueNumeric": 3,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a9881db7ba77479ba3887b",
      "questionType": "Net Promoter Score",
      "questionText": "How likely are you to recommend us to a friend or colleague?",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": 6,
      "valueNumeric": 6,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a9881db7ba77479ba3887b",
      "questionType": "Net Promoter Score Custom Answer",
      "questionText": "How likely are you to recommend us to a friend or colleague?",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": "qadw",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a98826b7ba77479ba3888b",
      "questionType": "Slider",
      "questionText": "Question 17",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": 3,
      "valueNumeric": 3,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a98835b7ba77479ba388b3",
      "questionType": "Thumbs",
      "questionText": "Question 18",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": "yes",
      "valueNumeric": 1,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a98838cb3cda478b556b6d",
      "questionType": "Text",
      "questionText": "Question 19",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": "+495678493123",
      "valueNumeric": 495678493123,
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a98842cb3cda478b556b77",
      "questionType": "Text",
      "questionText": "Question 20",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": "Wed Jun 08 2022 00:00:00 GMT+0300 (Eastern European Summer Time)---",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a98847b7ba77479ba388c3",
      "questionType": "Text",
      "questionText": "Question 21",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": "vb@fgh.com",
      "valueLabel": ""
    },
    {
      "surveyId": "62a98755b7ba77479ba386ff",
      "participantId": "62a98866b7ba77479ba38a11",
      "createdAt": "2022-06-15T07:21:10.252Z",
      "sectionId": "62a98755b7ba77479ba38700",
      "section": "",
      "questionId": "62a9884bcb3cda478b556b81",
      "questionType": "Country List",
      "questionText": "Question 22",
      "optionId": "",
      "optionName": "",
      "optionType": "string",
      "value": "Eritrea",
      "valueLabel": ""
    }
  ],
  "total": 1
}
```

### HTTP Request

`GET /api/v1/tableau/get-data`

### Query

| Parameter | Type          | Description                                                                                                                                                                                                                                                                                                            | Valid                         | Required |
|-----------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------|----------|
| surveyId  | string (ID)   | Get results by specific survey                                                                                                                                                                                                                                                                                         | any                           | No       |
| from      | string (date) | Param represents the date FROM which we will count the results. It can be represented as a simple date-string in format of MM-DD-YYYY or by number of milliseconds.                                                                                                                                                    | `03.10.2022`, `1655738381328` | No       |
| to        | string (date) | Param represents the date BEFORE which we will count the results. It can be represented as a simple date-string in format of MM-DD-YYYY or by number of milliseconds.                                                                                                                                                  | `03.10.2022`, `1655738381328` | No       |
| limit     | number        | Param represents the specification of the maximum number of survey's results the query will return.                                                                                                                                                                                                                    | any                           | No       |
| skip      | number        | Param represents the specification of the number of survey's results to skip.                                                                                                                                                                                                                                          | any                           | No       |
| sort      | string        | Param represents the value that all results will be sorted by. There are two types of sorting: ascending and descending. If you want to sort results in ascending order just specify the value. If you want to sort results in descending order, specify the value and add '-' before the value. Default: `-createdAt` | `-createdAt`, `createdAt`     | No       |

Filter params in combination.

As was mentioned before, we can use the combination of the different params to filter survey’s results properly.

For example, if we want to get only 10 results for survey with ID 62a9ac2ccebfa2c48701b38c which comes between 10 March 2022 and 15 March 2022 and sort them by creation date in descending order, the final query will looks like this:

`/api/v1/tableau/get-data?surveyId=62a9ac2ccebfa2c48701b38c&from=03.10.2022&to=03.15.2022&limit=10&sort=-createdAt`



Reminder
If you don’t specify any filter, the query will return all survey’s results related to your company for all surveys and sorts by default value -createdAt in descending order.
