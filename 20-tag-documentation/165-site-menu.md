#### `{% site_menu %}`

This outputs the site navigation in an unordered list, starting at the root level of the site.

### Attribute Options

`ul_class: "your-class"` - The class that the site menu should have.

`ul_id: "your-id"` - The ID that the site menu should have.

`li_class: "some-li-class"` - The class applied to each list item.

`link_class: "some-a-class"` - The class applied to each anchor tag in the list.

`max_depth: "number"` - The max depth that the site menu should go from the root level.

`active_class: "your-class"` - The class that gets added to the `<a>` tag of the page you are currently on.

`open_class: "your-class"` - The class that gets applied to every `<li>` tag containing the current page.

`has_children_class: "your-class"` - Adds a class to any `<li>` that contains and unordered list.

`sub_ul_class: "your-submenu-class"` - Adds a class to any `<ul>` at the second level or deeper. Also adds an additional class based on level. For example, if you named your class `your-submenu-class`, it's going to output `your-submenu-class your-submenu-class--level-1` for the first level. For nested `<ul>`'s two levels deep, it will output `your-submenu-class your-submenu-class--level-2`. View an [example of the markup](https://gist.github.com/wvuwebgist/d52ae8c96115c268ee57797f36438eb1) this tag generates.

`include_link_ids: "true"` - Boolean. Default value: `true`. Enables/disables output of ID's set via the Link Attributes tab in Page Properties on anchor tags (`<a>`).

### Example:

```
{% site_menu ul_class: "some-class", ul_id: "some-id", li_class: "some-li-class", link_class: "some-a-class", max_depth: "1", active_class: "active", open_class: "open", has_children_class: "your-class", sub_ul_class: "your-submenu-class", include_link_ids: "true" %}
```
