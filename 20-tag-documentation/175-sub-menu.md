#### `{% sub_menu %}`

Lists the child pages that are direct descendants of the current page as an unordered list.

So, if you had:

  * Parent 1
    * Child 1
    * Child 2
    * Child 3
  * Parent 2
  * Parent 3
    * Child 4
    * Child 5
    * Child 6
  * Parent 4

...and you put `{% sub_menu %}` on "Parent 1", it will list "Child 1", "Child 2", and "Child 3".

If you put `{% sub_menu %}` on "Parent 2", no pages would be listed.

### Attribute options

`ul_class: "your-class"` - The class that the unordered list will have.

`ul_id: "your-id"` - The ID that the unordered list will have.

`li_class: "some-li-class"` - The class applied to each list item.

`link_class: "some-a-class"` - The class applied to each anchor tag in the list.

`max_depth: "number"` - The number of levels from the root level that CleanSlate should list navigation for.

`active_class: "your-class"` - The class that gets added to the `<a>` tag of the page you are currently on.

`open_class: "your-class"` - The class that gets applied to every `<li>` tag containing the current page.

`has_children_class: "your-class"` - Adds a class to any `<li>` that contains and unordered list.

`sub_ul_class: "your-submenu-class"` - Adds a class to any `<ul>` at the second level or deeper. Also adds an additional class based on level. For example, if you named your class your-submenu-class, it's going to output your-submenu-class your-submenu-class--level-1 for the first level. For nested `<ul>`'s two levels deep, it will output your-submenu-class your-submenu-class--level-2. View an [example of the markup](https://gist.github.com/wvuwebgist/d52ae8c96115c268ee57797f36438eb1) this tag generates.

`include_link_ids: "false"` - Boolean. Default value: false Enables/disables output of ID's set via the Link Attributes tab in Page Properties on anchor tags (`<a>`).

<p style="font-size: .8rem; padding-left: 20px;"><strong>NOTE:</strong> Be careful enabling this on <code>sub_menu</code>. If you don't have this set to false on <code>site_menu</code>, <code>ancestor_menu</code>, and <code>breadcrumbs</code>, you will have duplicate ID's being output for the main navigation and ancestor navigation.</p>

### Example:

```
{% sub_menu ul_id: "some-submenu", ul_class: "menu", li_class: "some-li-class", link_class: "some-a-class", active_class: "active", open_class: "open", max_depth: "2", has_children_class: "your-class", sub_ul_class: "your-submenu-class", include_link_ids: "false" %}
```
