Data harvester
--------------

The Data Harvester collects data from a production database mirror on a protected network and sends it to the service end users see. It encrypts the data and then transfers it over SSL/TLS to the server.

The Data Harvester runs on Windows with .NET 4.

The Data Harvester can collate the data itself but the recommended approach is to use a native database job to put the data in a temporary “cache” table and the Data Harvester just does a simple select from there.

The required format for the data is as follows:

| Column name     | Data type     | Purpose                                                                                                                                                                         |
|-----------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Postcode        | varchar(9)    | This allows the approximate location to be plotted on a map                                                                                                                     |
| SalesValue      | money         | Second line of the map marker and totals for the heat map                                                                                                                       |
| DisplayText     | varchar(50)   | Comma separated list of text to display on map markers. This can be shown or the district the sale took place depending on settings.                                            |
| ProductImageUrl | varchar(150)  | Comma separated list of URLs or URL parts to show on the map marker.                                                                                                            |
| OrderDateTime   | timestamp     | Date and time order was entered into the source system.                                                                                                                         |
| OrderID         | varchar(100)  | Order identifier. Used for avoiding duplicates.                                                                                                                                 |
| MeasureID       | integer       | 1 for Sale, 2 for Return                                                                                                                                                        |
| OrderDetail     | varchar(2000) | Comma separated list of text to display when users hover over a map marker.                                                                                                     |
| ProductUrl      | varchar(500)  | Comma separated list of URLs or URL parts which are used when a user clicks on a map marker. This should allow linking to the product in question and in turn allow purchasing. |

By default, this is the SQL used:

`SELECT s.Postcode, s.SaleValue, s.DisplayText, s.ProductImageUrl, s.DateEntered as OrderDateTime, `
` s.OrderID, s.MeasureID, OrderDetail, ProductUrl `
`FROM sparkSales s`
`ORDER BY s.OrderID`

the sparkSales database object could be a real table or a view. A table being the recommended option. An example SQL Server script to collate this data is available [[SalesMap:setting up harvester sql]]