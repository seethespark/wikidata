## API ##
`GET` `/<page path>`
Requires headers x-application-id and x-service-key

Returns the content as JSON for the specified page path.
content is typically in the following format:
```json
{
docTitle: <title>, 
template: <template name>,
content: {<section name>: <section content>, ...}
}
```

`POST` `/<page path>`
Requires headers x-application-id and x-service-key

```
[{
	id: <element ID or "pageTitle" or "pageTemplate">,
	content: <element's content, probably text>
    image: <image name>
}]
```

`POST` `/applicationconfiguration`
Requires headers x-application-id and x-service-key

```
[{
	id: <element ID or "siteTheme">,
	content: <element's content, probably text>
    image: <image name>
}]
```

`GET` `/themes/<applicationId>`
Requires header x-service-key

`POST` `/applicationcon`
Requires headers x-application-id or applicationId as a parameter and x-service-key

Get a list of themes and associated info.  Themes can be specific to an organisation or they can be universal (organisation ID is NULL).

```json
{
name: <name>, 
value: <theme value for lookups, often the name with no spaces>,
variables: [{name: <theme specific variable name>, values[<value1>, <value2>...]}]
}
```

`DELETE` `/asset`
Requires headers x-application-id and x-service-key

If an image is deleted (probably from assetley) then check each Content entry and delete the corresponding image reference.