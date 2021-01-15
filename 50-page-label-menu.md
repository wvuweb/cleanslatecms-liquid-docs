# Page Label Menu

NOTE:

  * Removed "Note 2:" from Radius docs at the bottom here because I'm not sure how to only select pages at the root in Liquid. Solution?

This menu requires the following Liquid tags along with a standard HTML menu structure.

This starts us in the root of the site:

```
{% assign pages = site.pages %}
```

This selects all pages in your site that have been labeled `"name-of-your-label"`:

```
{% assign pages = site.pages | filter_pages: tags: "name-of-your-label" %}
```

Use the `<a>` tag with `{{ page.url }}` and `{{ page.name }}` to dynamically create the page link and name in the menu.

## Example:

```
{% assign pages = site.pages | filter_pages: tags: "name-of-your-label" %}
<ul>
  {% for page in pages.all %}
    <li>
      <a href="{{ page.url }}">{{ page.name }}</a>
    </li>
  {% endfor %}
</ul>
```

**Note:** Make sure the pages you're including in your Page Label Menu are _not_ hidden. Also, make sure they've been published.

**Note 2:** Want to use more than one label? Separate multiple labels with commas. Do not include a space. For example:
`tags: "first-label,second-label"`.
