This tag displays its content only if a blog doesn't have any articles.

### Example:

```
{% assign articles = blog.articles %}
{% if articles.length == 0 %}
  <p>No blog posts found. Try again later, perhaps?</p>
{% endif %}
```
