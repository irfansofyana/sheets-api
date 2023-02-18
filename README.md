# sheets-api
Make your Google Sheets into JSON API with free and easy!

## What is it?

sheets-api is basically a Google App Script library which can be used to make your Google Sheets into a JSON API. It has set of APIs that you can use to search, add, update, and delete from Google Sheets data.

This library is a good, easy to use, and free alternatives for some paid products like [SheetDB](https://docs.sheetdb.io/), [Sheetsu](https://sheetsu.com/) and others.

## Instalation

To install this library, you can create any Google Sheets and create an app script inside of it. After that, you will require to import following AppScript library `{{appscript_project_id}}`. You can use the latest version of this library.

After the import is success, you will need to create following AppScript Code

```
code xxxx
```

## List of APIs

### Insert Data

This API is used to insert data to a certain sheet name.

| Method | URL |
| ------ | --- |
| POST   | {{appscript_web_url}}


#### Request Body

| Parameter | Type | Required | Description |
| --------- | ---- | -------- | ----------- |
| action | string | mandatory | Must be set to "Insert" with case insensitive |
| sheetName | string | mandatory   | Sheet name where the data will be inserted |
| data      | array | mandatory  | Array of objects which will be inserted to the sheet. The keys of the object are the columns in the sheet and the value of the objects are the value that will be inserted |

#### Example Request:

```bash
curl --location 'https://script.google.com/macros/s/AKbcvfxUQKPcQokx8D_OcFC04FO1r36SJfWKKHayGOgEZ2DhYI26u10rdg51hRHTv5oUgAQabc/exec' \
--header 'Content-Type: application/json' \
--data '{
    "actionn": "Insert",
    "sheetName": "Sheet 1",
    "data": [
        {
            "first_name": "Irfan",
            "last_name": "Putra",
            "age": 23,
            "nationality": "Indonesia"
        }
    ]
}'
```

#### Example Response:

```JSON
{
    "status": "OK"
}
```

### Read Data

This API is used to read data from Google sheets.

| Method | URL |
| ------ | --- |
| GET    | {{appscript_web_url}}

#### Query Parameters


| Parameter | Type | Required | Description |
| --------- | ---- | -------- | ----------- |
| sheetName | string | required | Sheet name where the data will be read |
| action | string | optional | Can be set to "search" if you need to search specific data |
| limit | integer | optional | Limit the number of rows returned. If set, must be value > 0 |
| offset | integer | optional | How many rows to skip. If set, must be value > 0 | 

#### Example Request

```bash
curl --location 'https://script.google.com/macros/s/AKbcvfxUQKPcQokx8D_OcFC04FO1r36SJfWKKHayGOgEZ2DhYI26u10rdg51hRHTv5oUgAQabc/exec?sheetName=Sheet%201'
```

#### Example Response

```json
{
    "status": "OK",
    "data": {
        "columns": [
            "first_name",
            "last_name",
            "age",
            "nationality",
        ],
        "count": 2,
        "rows": [
            {
                "first_name": "irfan",
                "last_name": "Putra",
                "age": 23,
                "nationality": "Indonesia"
            },
            {
                "first_name": "Neymar",
                "last_name": "Junior",
                "age": 31,
                "nationality": "Brazil"
            }
        ]
    }
}
```

### Update Data

This API is used to update data to a certain sheet name.

| Method | URL |
| ------ | --- |
| POST   | {{appscript_web_url}}


#### Request Body

| Parameter | Type | Required | Description |
| --------- | ---- | -------- | ----------- |
| action | string | mandatory | Must be set to "Update" with case insensitive |
| sheetName | string | mandatory   | Sheet name where the data will be updated |
| singleUpdate | boolean | mandatory | The update operation mode whether it's single update or batch update. Set to `true` if it's single update otherwise it's batch update |
| query | object | conditional | Query to match for the rows that will be updated. Consist of `column` and `value` keys. `column` key is the column name and `value` is the value of the column that will be query. This field is mandatory if `singleUpdate` is true. |
| data | object | conditional | All rows match `query` before will be updated with this data. This field is mandatory if `singleUpdate` is true  |

#### Example Request:

```bash
curl --location 'https://script.google.com/macros/s/AKbcvfxUQKPcQokx8D_OcFC04FO1r36SJfWKKHayGOgEZ2DhYI26u10rdg51hRHTv5oUgAQabc/exec' \
--header 'Content-Type: application/json' \
--data '{
    "action": "Update",
    "sheetName": "Sheet 1",
    "singleUpdate": true,
    "query": {
        "column": "first_name",
        "value": "irfan"
    },
    "data": {
        "first_name": "IRFAN",
        "last_name": "PUTRA",
        "age": 25
    }
}'
```

#### Example Response:

```JSON
{
    "status": "OK"
}
```
