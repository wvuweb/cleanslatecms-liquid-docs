#### `get_page`

TODO:

  * Update paragraph two in Radius docs ("This tag is useful").
  * Update order of Attribute Options vs Example headings

Target a certain page by via ID. Most often used within a loop.

This tag is useful for pulling navigation into a different page on your site, pulling content from other pages or pulling student/staff profiles onto a homepage (likely in tandem with a `for` loop), among many other uses.

### Attribute options

`get_page` - Number. The page ID of the page you would like to target. The ID can be found by editing the target page and looking at the URL in your browser's address bar. It'll be something like `https://cleanslate.wvu.edu/sites/10/pages/1234/editor`. 👈 The ID for that page is `1234`.

### Examples

#### Target a specific page and get the page name:

```
{% assign page_about_bears = site | get_page: 77 %} <!-- Change this number to the ID of the page you want to target -->
<p>{{ page_about_bears.name }}</p>
```

#### Target a specific page and output some of it's properties (name, link, ID):

```
{% assign specialPage = site | get_page: 77 %}
<a href="{{ specialPage.url }}" data-page-id="{{ specialPage.id }}">{{ specialPage.name }}</a>
```

#### Target a parent page and output one of it's children:

```
{% assign nestedPage = site | get_page: 77 %}
<p>{{ nestedPage.children.first.name }}</p>
```

**Note:** Besides `.first`, you can also use `.last`.

#### Target a parent page and loop through it's children:

```
{% comment %} get_page: 77 = ID of a parent page with children {% endcomment %}
{% assign parentPage = site | get_page: 77 %}
<ul>
  {% for page in parentPage.children.all %}
    <li>
      <a href="{{ page.url }}" data-page-id="{{ page.id }}">{{ page.name }}</a>
    </li>
  {% endfor %}
</ul>
```

**Note:** `parentPage.children.all` could also be `parentPage.siblings.all`, `parentPage.descendants.all` or `parentPage.ancestors.all`.

#### Target a blog index and output a list of blog posts:

```
{% assign blog = site | get_page: 123 %} <!-- Change this ID to your blog_index page's ID -->
{% assign articles = blog.articles | filter_articles: limit: 5 %}
{% for article in articles.all %}
  <article class="wvu-article">
    <h2 class="wvu-article__title"><a href="{{ article.url }}">{{ article.name }}</a></h2>
    <div class="wvu-article__body">
      {{ article.content['article-body'] | select_html: css_selector: 'p', limit: 1 }}
    </div> <!-- /.wvu-article__body -->
  </article> <!-- /.wvu-article -->
{% endfor %}
```

**Note:** See our [Blog Templates](https://cleanslatecms.wvu.edu/how-to/theme-development/blog-templates) page for more examples like this.
