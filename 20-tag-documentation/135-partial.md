#### `{% render %}`

Include a partial in your theme.

### Attribute options

`name: "name-of-partial"` - The name of the partial to include. The path is always from the root `views` directory.

**Note:** If you want to reference a partial with a different file extension than the one you're currently calling from (probably `.html`), simply add the extension onto the end of the filename (eg: `{% render "feed.json" %}`).

**Note 2:** Shared partials in Liquid do not need a `theme` attribute. The system will automatically detect if a partial is a shared partial if it cannot find the partial from within your theme. If the partial does not exist within your theme, the system then looks for the partial in the themes you've specified in your theme's `config.yml` under the `import_themes` key.

### Examples:

For a partial named  `_footer.html`:

```
{% render name: "footer" %}
```

This tag also doesn't require you to specify the `name` attribute. You will frequently see it omitted:

```
{% render "footer" %}
```

Calling `_footer.html` from inside `views/custom-patterns`:

```
{% render "custom-patterns/footer" %}
```
