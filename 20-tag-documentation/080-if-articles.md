This tag displays its contents if the blog has at least one article.

### Example:

```
{% assign articles = blog.articles %}
{% if articles.length > 0 %}
  <p>There is at least one blog post!</p>
{% else %}
  <p>No blog posts found. Try again later, perhaps?</p>
{% endif %}
```
