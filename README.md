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
| POST   | {{appscript_web_url}}/insert


| Parameter | Type | Required | Description |
| --------- | ---- | -------- | ----------- |
| sheetName | string | true   | Sheet name where the data will be inserted |
| data      | array | true  | array of object which will be inserted to the sheet. The keys of the object are the columns in the sheet and the value of the objects are the value that will be inserted |

Example Request:

```bash
curl --location 'https://script.google.com/macros/s/AKbcvfxUQKPcQokx8D_OcFC04FO1r36SJfWKKHayGOgEZ2DhYI26u10rdg51hRHTv5oUgAQabc/exec' \
--header 'Content-Type: application/json' \
--data '{
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


Example Response:

```JSON
{
    "status": "OK"
}
```