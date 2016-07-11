Settings can take up to 6 minutes to appear in the browser. The exception is Operation Mode which will take effect at the next browser poll (typically 1 minute).

Once you have updates the settings press Save or use the keyboard short-cut Ctrl + S

### Operation mode

-   Off stops people from receiving sales information. This will show a message in the connecting browser window.
-   Dev will always show something even if no new sales are being added, it picks 10.
-   Live shows sales added in the last few seconds, as dictated by the poll interval

### Poll interval

How often the end users' browser should check for new sales. There is rarely any need to change this.

### Previous sales lists to keep on client

The end users' browser can keep previous lists of sales if it is likely that some sales will be sent more than once. The current Sales Map doesn't send sales more than once but with some setups it can. If your original data time-stamping is not very accurate then this might become useful.

### Show client settings

Display a bar at the bottom of the client page which allows people to select their map, marker size and what measure is displayed. End user browsers must be refreshed for this setting to take effect.

### Allow Google map

This enables the Google map to work on the following setting. It inserts the appropriate javascript into the relevant pages. If this is false and Google maps are selected then end users will get errors. End user browsers must be refreshed for this setting to take effect.

### Google Maps key

The “key” supplied by Google to allow their map to be used. This can be obtained from Google's admin pages. You must also allow www.seethespark.com as a referrer in Google's admin page. By default, Sales May works with v3 of Google's API. If you are using an older version (i.e. the url is maps.google.com rather than maps.googleapis.com) then the whole URL must be entered.

### Map to display

Select the map the end users will see.

### Display text source sales

Where to get the text shown above the product image on map markers. It can come from the source database or the postcode district.

### Display text source returns

Where to get the text shown above the product image on map markers when Returns are selected. It can come from the source database or the postcode district.

### Image path base format

The path to the product images. %image\_name% is a variable so the path might be http://www/my-site.com/images/img%image\_name%.jpg. %image\_name% will be replaced by the path information received from the database.

### Click thorough URL base format

The path for destination when products are clicked. %productId% is a variable so http://www/my-site.com/prod/%productId% would link to the product specified by the database.

### Log client errors

If the users' browser throws an error then log it.
### Log all connections

Log every time a browser makes a connection. This includes every poll for new sales.

### Error server

Connection string for the error server. If you don't know what this is then don't change it.

### System message

Banner at the top of the page informing people of problems or upgrades. The banner is not shown if this box is blank.

### Map Marker Detail Call To Action

Text at the bottom of the map marker when the cursor is hovered over it.

### Show left panel

Show or hide the main information panel. End user browsers must be refreshed for this setting to take effect.

### Left panel heading

Left text panel heading.

### Left panel body

Left panel main text. HTML characters are allowed but please use sparingly.

### Logo

Upload the logo image for the top left corner.

### Missing image default

Upload an image for missing images. If product images fail to load then this image will be displayed.

------------------------------------------------------------------------

### Change password

Passwords must be at least 5 characters. There are no other restrictions.