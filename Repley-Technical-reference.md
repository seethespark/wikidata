__This page is expected to be used in conjunction with the the JSDoc generated documentation.__

## Caching ##
Reports are usually cached.  This serves two purposes, the first allows multi page reports to be paginated correctly.  The second allows miltiple runs of the same data to return quickly.

## Report request process ##
Reports consist of a report and report detail sections.  The report has an overall layout, a name, permissions and an validity dates.  Detail elements have queries, connections and layouts.  
On receiving a request for a report the server the report engine follws the following process.
* gets the header info and the sections from a database.
* check the defineitions of parameters are OK.  Parameters are defined using JSON so can get corrupted.
* check the parameters have been supplied.  If not show the parameters page.
* if parameters are supplied then start running the queries.  This uses the rows retrieved from the reports query mentioned above.
* loop through the passed in query rows and build an execution list.  This list can be run in series or paralell depending on opetions passed in.
* hash the organisationID, query and parameters to get a unique reference for the query.
* look up the query by its hash in the cache table.
* if no cached version is available then run the SQL provided in the query against the connection supplied.  query.js allows for a standardised interface for different database systems.  Currently only SQL Server and Postgres but easily extendable.
* store the result rows in cache and return the dataset.  This is done after results have been returned so the end user won't be informed if it fails.
* extract the column names from each dataset as the typical approach of database drivers id to return an array of row objects. 
* convert row objects to arrays.  This and the prevous step give a report object with an array of columns and an array of row arrays.
* loop through the datasets and the original report definition.  Get the section definition so the dataset can be turned inot HTML.  If column mappings are defined the HTML will be modified to take this into account. If the number or rows exceeds the report section definition allowed value the dataset is paginated.  It checks if it is 2 over so as not to have a second page with just one row as that's annoying.
* combine the HTML chunks together and present on the overall report master templete.