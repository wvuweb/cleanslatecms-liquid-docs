#### `{% ancestor_menu %}`

This will list all pages going up from the current page and pages at the root. So, if you put this tag in a page nested deep within your site, it will print out all pages above and below the current page. It will not print out pages nested beneath other root level pages.

### Attribute options

`ul_class: "your-class"` - The class that the unordered list will have.

`ul_id: "your-id"` - The ID that the unordered list will have.

`active_class: "your-class"` - The class that gets added to the `<a>` tag of the page you are currently on.

`open_class: "your-class"` - The class that gets applied to every `<li>` tag containing the current page.

`start_depth: "number" `- Page depth to start listing pages from. Defaults to current page depth. Cannot exceed current page depth.

`max_depth: "number"` - Maximum number of levels to list.

`include_link_ids: "false"` - Boolean. Default value: `false`. Enables/disables output of ID's set via the Link Attributes tab in Page Properties on anchor tags (`<a>`).

<p style="font-size: .8rem; padding-left: 20px;"><strong>NOTE:</strong> Be careful enabling this on <code>ancestor_menu</code>. If you don't have this set to false on <code>site_menu</code>, <code>sub_menu</code>, and <code>breadcrumbs</code>, you will have duplicate ID's being output for the main navigation and ancestor navigation.</p>

### Example:

```
{% ancestor_menu ul_id: "ancestor", ul_class: "menu", start_depth: "1", max_depth: "2", active_class: "active", open_class: "open", include_link_ids: "false" %}
```
