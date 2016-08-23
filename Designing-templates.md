Templates must follow certain patterns in order for their regions to be editable by other users.  

All `<article>` elements are editable unless they have a "notEditable" class added.
All elements with the class "editable" are editable.

The ID of an element is used to link the content to the DOM element.

All See The Spark sites currently (as of July 2016) use Handlebars templating so HTML is mixed with {{}} tags.

An example of a valid, editable element is:
`<div id="foo">{{content.foo}}</div>`

`<p>` tags don't work well so it is better to use divs.

When creating layout pages the content should reside in the applicationContent object.  This is available in all pages.  A vaild, editable element in a layout is:
`<div id="foo">{{applicationContent.foo}}</div>`