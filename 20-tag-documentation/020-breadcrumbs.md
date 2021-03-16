#### `{% breadcrumbs %}`

This tag outputs site breadcrumbs in an unordered list.

### Attribute Options

`ul_id: "your-id"` - The ID that the unordered list should have.

`ul_class: "your-class"` - The class that the unordered list should have.

`link_class: "your-anchor-class"` - Apply classes to each anchor tag (`<a>`) in the unordered list.

`include_link_ids: "false"` - Boolean. Default value: `false`. Enables/disables output of ID's set via the Link Attributes tab in Page Properties on anchor tags (`<a>`).

<p style="font-size: .8rem; padding-left: 20px;"><strong>NOTE:</strong> Be careful enabling this on <code>breadcrumbs</code>. If you don't have this set to false on <code>site_menu</code>, <code>sub_menu</code>, and <code>ancestor_menu</code>, you will have duplicate ID's being output for the main navigation and ancestor navigation.</p>

### Example:

```
{% breadcrumbs ul_id: "my-breadcrumbs-id", ul_class: "wvu-breadcrumbs__crumbs", link_class: "your-anchor-class", include_link_ids: "false" %}
```
