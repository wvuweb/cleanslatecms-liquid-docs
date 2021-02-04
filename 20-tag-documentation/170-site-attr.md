#### `site.{attr}`

TODO:

  * Shore up docs for `first_random_image_tagged_with` and `background_styler`
  * Shore up description for `root_page`.
  * Learn/write docs for `base_pages`
  * Add example / link to docs for `get_file` and `files`.

Use this tag to get properties about the current site, where {attr} is replaced by one of the attributes listed below.

### Attribute options

`id` - Get the site ID

`name` - Get the site name

`root_page` - Get the root page of the site (Note: this is not the homepage and is hidden to all users). Returns an array.

`domain` - Get the domain for the site. Returns: `example.wvu.edu`.

`url`: Get the canonical URL for the site. Returns: `https://example.wvu.edu`

`first_random_image_tagged_with` - Get a random image that has been tagged with the specified label.

`background_styler` - Add a background image via inline CSS. The background image must have a label and will be output with dimensions of 1780x1780.

`get_page` - Get a specific page via it's ID. See the documentation for [`get_page`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-get-page).

`pages` - Returns an array of every page in your site.

`base_pages` - ?

`get_file` - Get a file via file ID. Find a file's ID by going to Files and hovering over the preview. The ID will show up in the `title` text.

`files` - Get an array of all the files in a site.

`data` - Access Custom Site Data. See our documentation for [Custom Site Data](https://cleanslatecms.wvu.edu/how-to/theme-development/custom-data#custom-site-data).

### Examples

Get a site ID:

```
{{ site.id }}
```

☝️ You can use this format for `id`, `name`, `domain` and `url`.

Access Custom Site Data:

```
{{ site.data.my_site_data_name }}
<!-- OR -->
{{ site.data["my_site_data_name"] }}
```

Get a specific page using `get_page`:

```
{% assign pages = site.pages | get_page: 77 %}
{% for page in pages.all %}
  <p>{{ page.name }}</p>
{% endfor %}
```

Get one random page that has any of the following labels:

```
{% assign pages = site.pages | filter_pages: labels: "test-label,a-label", limit: 1, random: true %}
<ul>
  {% for page in pages.all %}
    <li>
      <a href="{{ page.url }}">{{ page.name }}</a>
    </li>
  {% endfor %}
</ul>
```
