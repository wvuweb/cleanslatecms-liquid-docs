#### `blog.{attr}`

This is not truly a tag, but rather a format you would use to get properties about the blog post or index, where `attr` is replaced by the information you are retrieving. For some "real world" uses of `blog.{attr}`, see our page on [Blog Templates](https://cleanslatecms.wvu.edu/how-to/theme-development/blog-templates).

`blog.{attr}` _must_ be used on a Blog Index or Blog Article page type. Or, it must be used in a loop inside of the blog context (likely via `get_page`).

Most of the attribute options available for [`page.{attr}`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-page) are **also available for `blog.{attr}`**. The attributes listed below are `blog.{attr}` specific attributes:

### Attribute options

`articles` - Refers to the articles drop. See our documentation for [`article.{attr}`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-article-attr) for more information.

`months_archive` - Parent tag used to build an monthly blog archive. Returns an array. When used in a loop, the first item in the array (at position `0`) reutrns the year and month (eg: `2021/1`). The second item in the array (position `1`) returns how many blog posts were made in that month.

### Examples

Just like `page.{attr}`, you can use many of the same attributes for `blog.{attr}`:

```
{{ blog.id }} <!-- 1234 -->
{{ blog.name }} <!-- Blog -->
{{ blog.slug }} <!-- blog -->
{{ blog.author.full_name }} <!-- May Day -->
<!-- ...and many more... -->
```

A blog archive:

```
<h3>Archives</h3>
{% if blog.months_archive.size > 0 %}
  <ul class="wvu-blog-archive">
    {% for entry in blog.months_archive %}
      <li>
        <a class="wvu-blog-archive__month-year" href="{{ blog.url | append: '/' | append: entry[0] }}">
          {{- entry[0] | date: "%B %Y" -}}
        </a>
        <span class="wvu-blog-archive__posts-in-month">({{ entry[1] }})</span>
      </li>
    {% endfor %}
  </ul>
{% endif %}
```

In the example above, `{{ entry[0] }}` returns `2021/1` and `{{ entry[1] }}` returns `n` where `n` is the number of blog posts for that month.
