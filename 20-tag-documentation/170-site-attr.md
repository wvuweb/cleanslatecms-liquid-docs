#### `site.{attr}`

Use this tag to get properties about the current site, where {attr} is replaced by one of the attributes listed below.

### Attribute options

`id` - Get the site ID

`name` - Get the site name

`root_page` - Get the root page of the site (Note: this is not the homepage and is hidden to all users). Returns an array.

`domain` - Get the domain for the site. Returns: `example.wvu.edu`.

`url`: Get the canonical URL for the site. Returns: `https://example.wvu.edu`

`first_random_image_tagged_with` - Get a random image that has been tagged with the specified label. See [Get a random image, file, or blog article](https://cleanslatecms.wvu.edu/how-to/theme-development/random-image-file-or-blog-article) for more information.

`background_styler` - Add a background image via inline CSS. The background image must have a label and will be output with dimensions of 1780x1780. See [Get a random image, file, or blog article](https://cleanslatecms.wvu.edu/how-to/theme-development/random-image-file-or-blog-article) for more information.

`get_page` - Get a specific page via it's ID. See the documentation for [`get_page`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-get-page).

`pages` - Returns an array of every page in your site. See the documentation for [`r:page:{attr}`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-page).

`base_pages` - Get an array of the pages at the top/root level of a site.

`get_file` - Get a file via file ID. Find a file's ID by going to Files and hovering over the preview. The ID will show up in the `title` text. See [`r:get_file`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-get-file) for more information on this tag.

`files` - Get an array of all the files in a site. See the documentaiton for [`r:files`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-files-attr).

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

Make a list of all pages at the top level of a site:

```
{% assign rootPages = site.base_pages %}
<ul>
  {% for page in rootPages.all %}
    <li>
      <a href="{{ page.url }}">{{ page.name }}</a>
    </li>
  {% endfor %}
</ul>
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
