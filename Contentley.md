## API ##
GET /<page path>
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

GET /applicationconfiguration
Requires headers x-application-id and x-service-key

Returns the app config for "Sites" application

POST /applicationconfiguration
Requires headers x-application-id and x-service-key
Requires 'layout' for inserts
Requires 'layout' or 'description' for updates