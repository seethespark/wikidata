[[Designing templates]]

## Adding a new page ##
Navigate to the page you want to edit and then add a suffix "content", so http://example.com/home becomes http://example.com/home/content

Change the template at the bottom.  Always change it even if you change it back as the default isn't saved.

Make a change in a blue outlined box.

Save!

Go back to the original page and check.

By convention, the default site page, `/`, is accessed via the index/content so http://example.com/ becomes http://example.com/index/content 

## Editing page content ##
You must be in the contentEditor group.

You can only edit content of pages which the side developers have allowed.

Either use the Admin dashboard at /admin or navigate to `http://site/pagePath/content`.

Edit the text content.  Click on the `</>` button to edit the HTML directly.

Click save.

To change the page title scroll to the bottom of any editable page and change the title section.  If it has a leading space then remember to delete that after you have added the title.  This is a bug but bear with us for now.

The template can be changed but changing it to an invalid value will break the page.

All changes take effect immediately on the server but browsers will use cached content for a period of time.