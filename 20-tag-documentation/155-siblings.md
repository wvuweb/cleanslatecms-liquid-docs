#### `page.siblings`

A tag used to loop through sibling pages.

**Note:** this tag is technically part of the `page.{attr}` drop. Be sure to check out the documentation for [`page.{attr}`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-page).

### Attribute options

`previous_sibling` - Get the previous sibling. Returns an array. Use another drop to get the information you want (eg: `page.previous_sibling.url`)

`next_sibling` - Get the next sibling. Returns an array. Use another drop to get the information you want (eg: `page.next_sibling.name`)

### Examples

```
{{ page.previous_sibling.url }} <!-- https://example.wvu.edu/regular-page -->
{{ page.next_sibling.name }} <!-- How to Apply -->
```

Make a "Previous Page / Next Page" pager:

```
<ul class="pager">
  <li class="previous"><a href="{{ page.previous_sibling.url }}">&larr; {{ page.previous_sibling.name }}</a></li>
  <li class="next"><a href="{{ page.next_sibling.url }}">{{ page.next_sibling.name }} &rarr;</a></li>
</ul>
```

Get three sibling pages using a loop:

```
{% assign siblings = page.siblings | filter_pages: limit: 3 %}
<ul>
  {% for sibling in siblings.all %} <!-- or siblings.first / siblings.last -->
    <li><a href="{{ sibling.url }}">{{ sibling.name }}</a></li>
  {% endfor %}
</ul>
```

**Note:** You can also use `descendants`, `ancestors`, `children` on the page drop. Eg `page.siblings` would become `page.descendants`.
