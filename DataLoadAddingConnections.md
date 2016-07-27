## Database direct ##
This is fairly spef explanatory.  DataLoad supports several database types.  Input a valid connection string.  The password will be hidden next time you come to this page and must be input every time the connection string changes.

## REST API ##
Dataload is quite pedantic about how data should come from a RESTful API.  The source must have the following structure.

```json
{
"columns": [{"name": "<column 1 name>", "type": "<data type>"}, {...}],
"rows": [
["<row 1 column 1 value>", "<row 1 column 2 value>"], 
["<row 2 column 1 value>", "<row 2 column 2 value>"],
[...]
]
```

The Server Type should be WebJson.
The connection string is the URL to the source server.  The schema, table name and last updated timestamp (a big integer value of milliseconds sonce 01/01/1970) are appended to hte URL.