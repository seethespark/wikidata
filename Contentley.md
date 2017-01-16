## API ##
**`GET`** `/<page path>`
Requires headers x-application-id and x-service-key

<page path> is expected to have a trailing /content as the update usually comes from a URL with this pattern.  The /content is removed.  

The index or default page, "/", should be replaced with "/index" for clarity.

Combining the two previous statements, to modify "/" the actual <page path> should be "/index/content" just as it is in the UI.

Returns the content as JSON for the specified page path.
content is typically in the following format:
```json
{
docTitle: <title>, 
template: <template name>,
content: {<section name>: <section content>, ...}
}
```

**`POST`** `/<page path>`
Requires headers x-application-id and x-service-key

Holds content information about a single page.  Page title, images and text.

```javascript
[{
	id: <element ID or "pageTitle" or "pageTemplate">,
	content: <element's content, probably text>
    image: <image name>
}]
```
Returns {message: 'OK'} or an error

**`POST`** `/applicationconfiguration`
Requires headers x-application-id and x-service-key

Holds the application level content information.  Things like theme or layout level content whcich is shared across many pages

```javascript
[{
	id: <element ID or "siteTheme">,
	content: <element's content, probably text>
    image: <image name>
}]
```
Returns {message: 'OK'} or an error

**`GET`** `/themes/<applicationId>`
Requires header x-service-key

**`POST`** `/applicationcon`
Requires headers x-application-id or applicationId as a parameter and x-service-key

Get a list of themes and associated info.  Themes can be specific to an organisation or they can be universal (organisation ID is NULL).

```json
{
name: <name>, 
value: <theme value for lookups, often the name with no spaces>,
variables: [{name: <theme specific variable name>, values[<value1>, <value2>...]}]
}
```

**`DELETE`** `/asset`
Requires headers x-application-id and x-service-key

If an image is deleted (probably from assetley) then check each Content entry and delete the corresponding image reference.