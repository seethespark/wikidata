This application uses C as the prefix for all errors. The following two digits relate to where the page sits in the application.

| Code prefix | File              |
|-------------|-------------------|
| C01         | app.js            |
| C02         | admin.js          |
| C03         | api.js            |
| C04         | apipiblic.js      |
| C05         | customers.js      |
| C06         | users.js          |
| C07         | db.js             |
| C08         | index.js          |
| C09         |                   |
| C10         |                   |
| C11         | lib/systeminfo.js |
| C12         |                   |

| Code   | Description                                                                                         |
|--------|-----------------------------------------------------------------------------------------------------|
| C11001 | System Info select database error.                                                                  |
| C02003 | getData helper method                                                                               |
| C02005 | getChartData helper methos                                                                          |
| C02007 | Checking to see if SystemInfo entry already exists                                                  |
| C02008 | Inserting or updating SystemInfo                                                                    |
| C02009 | More than one SystemInfo row updated                                                                |
| C02006 | Uncaught systemInfo update                                                                          |
| C02010 | Invalid SystemInfo setting                                                                          |
| C02016 | SystemInfo put error                                                                                |
| C02012 | admin page set password update error                                                                |
| C03008 | saveSales received error                                                                            |
| C03009 | saveSales more than one row updated                                                                 |
| C03001 | user.authenticate callback error                                                                    |
| C03002 | saveSales callback error                                                                            |
| C03007 | saveSales more than one error received                                                              |
| C03010 | AES key on client doesn't match server version                                                      |
| C03003 | sale data decryption error                                                                          |
| C03004 | uncaught sale receiving error                                                                       |
| C03006 | username not received by API                                                                        |
| C03005 | empty body received by API                                                                          |
| C03011 | empty data array received by API. Message received correctly but the dataset had 0 rows.            |
| C04002 | getSales helper function database error                                                             |
| C04008 | getSystemInfoData database error                                                                    |
| C04009 | getSystemInfoData uncaught error                                                                    |
| C04099 | System switched off                                                                                 |
| C04020 | maxdate not sent to the /sales path (format /apipublic/sales/maxDate/measure                        |
| C04021 | maxdate must be a number                                                                            |
| C04022 | measure must be a number                                                                            |
| C04016 | getSales database error                                                                             |
| C04001 | getSales uncaught error                                                                             |
| C04024 | order ID must be supplied to /sale/:orderId/:productNumber                                          |
| C04025 | order ID must be an integer (this isn't enforced in the database so may be removed at a later date) |
| C04026 | product ID must be a number(this isn't enforced in the database so may be removed at a later date)  |
| C04005 | order ID lookup failed. This shouldn't happen in normal operation.                                  |
| C04006 | Unable to receive order specific data                                                               |
| C04018 | getSystemInfo systemInfo is not an array                                                            |
| C04010 | error received from client                                                                          |
| C04035 | request body is badly formed after decryption - i.e. can't retrieve ERRORCODE after parsing JSON    |
| C04034 | request body is badly formed for unencrypted post- i.e. can't retrieve ERRORCODE after parsing JSON |
| C04028 | save sale callback error                                                                            |
| C04029 | no data received in payload                                                                         |
| C04030 | customer ID lookup not working                                                                      |
| C04031 | no body received                                                                                    |
| C04032 | other sale receiving error                                                                          |
| C04033 | getcountysalestoday database error                                                                  |
| C08001 | rendering Salesmap home page error                                                                  |
| C06002 | user update load user callback error                                                                |
| C06003 | A user with insufficient privileges attempted to change a user                                      |
| C06004 | user put load user callback error                                                                   |
| C06005 | A user with insufficient privileges attempted to add a user                                                                   |
| C06006 | user deleteload user callback error                                                                   |
| C06007 | A user with insufficient privileges attempted to delete a user                                                                  |