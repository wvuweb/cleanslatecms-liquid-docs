#### `{{ "<p>Hello world</p>" | select_html: css_selector: "p", limit: 1 }}`

A Liquid Filter to select HTML from a string. This Filter is most often used when looping through content on pages via [`for` loops](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-loop).

### Attribute options

`css_selector` - String. Pass this attribute any valid CSS selector (eg: `h2` or `.example`). Separate multiple selectors with commas and spaces.

`limit: 3` - Number. Limits how many tags to return.

Examples:

```
{{ "<p>Hello world</p><p>This is content</p>" | select_html: css_selector: "p", limit: 1 }}
<!-- Output: "<p>Hello world</p>" -->
```

```
<!-- Used within a `for` loop: -->
{{ article.content["article-body"] | select_html: css_selector: ".article-thumbnail, p", limit: 2 }}
```

See an example of this in the CleanSlate Toolkit's [Blog Index template](https://github.com/wvuweb/cleanslate-toolkit/blob/liquid/views/blog_index.html#L25).
