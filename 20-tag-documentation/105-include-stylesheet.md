#### `{% link_stylesheet %}`

Stylesheets _must_ be stored in the `stylesheets` directory.

To include a file called `styles.css`, use this syntax:

```
{% link_stylesheet name: "styles" %}
```

Do not include the `.css` extension when adding file names.

You can also include multiple stylesheets by separating them with commas. For example, if you wanted to add three files named `bootstrap.min.css`, `main.css`, and `ie.css`, add them like so:

```
{% link_stylesheet name: "bootstrap.min, main, ie" %}
```

For files in subdirectories inside your `stylesheets` directory, include the path like this:

```
{% link_stylesheet name: "path/to/stylesheet" %}
```

If you have multiple stylesheets at different paths, include them like this:

```
{% link_stylesheet name: "path/to/stylesheet, example-1, dist/main" %}
```

## Attribute options

`name: "stylesheet-name"` - The name(s) of the stylesheet(s) in the `stylesheets` directory, without the `.css` suffix.

## Example

One file:

```
{% link_stylesheet name: "main" %}
```

Multiple files:

```
{% link_stylesheet name: "skeleton, styles, custom" %}
```
