#### `{% if edit_mode %}`

This tag should wrap content that you only want to show when editing a page. Any content within this tag will not be shown when the page is viewed outside the editor.

The content will not be hidden with CSS - the content will actually not be parsed by the server, which means it won't show up in the HTML source.

### Example:

```
{% if edit_mode %}
  <p>I only want to see this when editing the page.</p>
{% endif %}
```

#### Not edit mode:

You can also do the inverse: only show something in production but _not_ in edit mode:

```
{% unless edit_mode %}
  <p>I only want to see this in production and <em>not</em> in edit mode.</p>
{% endunless %}
```

You could also write the above using `if` and a few more characters:

```
{% if edit_mode != true %}
  <p>I only want to see this in production and <em>not</em> in edit mode.</p>
{% endif %}
```

Why would you want to do this? Sometimes, you may have JavaScript that modifies DOM elements on page load. If this happens in edit mode, you could inadvertently save content altered by JavaScript to the editable region/database that you might not want to save.

An example of this is this very site. This site uses [Prism.js](https://prismjs.com/) for syntax highlighting. This library adds `span`'s and classes to the DOM to color code snippets. We don't want to change the DOM in edit mode, so we could use `{% unless edit_mode %}` for this task.
