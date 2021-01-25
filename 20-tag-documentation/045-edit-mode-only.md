#### `{% if edit_mode %}`

This tag should wrap content that you only want to show when editing a page. Any content within this tag will not be shown when the page is viewed outside the editor.

The content will not be hidden with CSS - the content will actually not be parsed by the server, which means it won't show up in the HTML source.

### Example:

```
{% if edit_mode %}
  <p>I only want to see this when editing the page.</p>
{% endif %}
```
