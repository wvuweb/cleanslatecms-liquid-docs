#### `article.{attr}`

Like [`page.{attr}`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-page), this is not a tag by itself but rather a collection of tags that allow you to display information about a blog article.

`article.{attr}` _must_ be used on a Blog Article or Blog Index page type. Or, it must be used in a loop inside of the blog context (likely via `get_page`).

`article.{attr}` accepts all of the same attributes as `page.{attr}`. Please reference the `page.{attr}` documentation for a complete list of available attributes—just be sure to replace `page` with `article`. Eg: `{{ page.id }}` becomes `{{ article.id }}`.

### Examples

```
{{ article.id }} <!-- 138 -->
{{ article.name }} <!-- Sally's Delicious Sweets -->
{{ article.slug }} <!-- sallys-delicious-sweets -->
{{ article.author.full_name }} <!-- May Day -->
{{ article.published_at | date: "%A, %B %d, %Y" | default: "Not Yet Published" }} <!-- Friday, January 15, 2021 -->
<!-- ...and many more... -->
```

Getting content from an editable region in a blog post:

```
{{ article.content["article-body"] | select_html: css_selector: "p", limit: 2 }}
```

If you want to use the code above on a Blog Index page, be sure to use it inside of a `for` loop.

See an example of `article.{attr}` being used in the [CleanSlate Toolkit](https://github.com/wvuweb/cleanslate-toolkit/blob/liquid/views/blog_index.html#L21-L27).
