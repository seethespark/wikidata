### What is Assetley ###
Assetley is a storage and delivery system for digital assets.  That's images and documents to you and me.

### By URL ###
To access an asset by URL you have to pass in a *key* and the application ID.
For example, application ID 3's image for the user with key *spark*:
https://assetley.seethespark.com/spark/3/sts-logo-small.png

### For proxying by another application ###
`GET` `/<file name>`
Requires a service key and application ID headers.
The most recent version of a file is sent.