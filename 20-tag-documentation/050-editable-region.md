#### `{% editable_region %}`

Inserts an editable region into your page. This is the lifeblood of CleanSlate and one of its core functionalities.

### Default content

You can add default content by using the `{% editable_region_block %}` tag:

```
{% editable_region_block name: "region-name" %}
  This is the default content
{% endeditable_region_block %}
```

### Attribute options

`name: "region-name"` - This must exist for every editable region so that the database can save the data. This is the name of the editable region. This may not have any spaces, punctuation or upper case letters. Each editable region name on a page/template must be unique.

`type: "simple"` - Turns the editable region into a plain-text region. It won't have code editor or WYSIWYG capabilities. In other words, the styles in this region won't be able to be changed by the user. They can only enter plain text.

`placeholder: "Example text"` - Adds default content into the editable region when you first open a page in edit mode.

`scope: "site"` - Makes the editable region global, meaning that the content inside the editable region will stay the same across every page where it exists. This is appropriate for content that stays the same between all pages, like header and/or footer content.

<p style="padding-left: 20px;"><strong>NOTE:</strong> If you make an editable region, then later decide to make it an editable region with global content, give the region a new name in the <code>name: "region-name"</code> field to avoid confusion in the CleanSlate database (and on your pages!).</p>

### Examples:

```
{% editable_region name: "main" %}
```

```
{% editable_region name: "phone_number", type: "simple" %}
```

```
{% editable_region name: "sidebar-1", placeholder: "I will be default content." %}
```
