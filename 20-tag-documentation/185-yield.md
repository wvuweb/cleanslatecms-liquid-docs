#### `{{ content_for }}`

This is a tag specific to Layouts. It indicates where the template will insert its data. [What are Layouts & r:yield?](https://cleanslatecms.wvu.edu/how-to/theme-development/getting-started-guide/what-are-layouts-and-r-yield)

Also read our page on [yielding content to other places within the DOM and Layout](https://cleanslatecms.wvu.edu/how-to/theme-development/yield-content-to-other-places).

This tag is particularly useful for including specific CSS or JavaScript files in a template or partial and inserting them in the `<head>` or just before the closing `</body>` tag (or anywhere in your layout you like).

### Attribute options

This tag doesn't have any attributes associated with it; however, it does require a name in quotes (`"content-name"`) directly after the tag.

### Example

Add this to your Layout (eg: default.html):

```
{{ content_for.page_js }}  <!-- 👈 This is where the content will output in your Layout. -->
```

And add to your template or partial:

```
{% content_for "page_js" %}
  <!-- Your content goes here -->
{% endcontent_for %}
```

**Note:** `page_js` can be any name (eg: `bears`, `flying-monkeys`, `headerExtraContent`, etc). If you change it in the `{% content_for %}` tag, make sure you also change it in the `{{ content_for }}` tag in your layout.

### What's the difference between `{{ content_for }}` and `{{ __TEMPLATE_CONTENT__ }}`?

`{{ __TEMPLATE_CONTENT__ }}` is a special tag that tells CleanSlate where to output the data from your template (eg: `frontpage.html` or `backpage.html`). When you create a page in the CleanSlate UI, users have the ability to select a template. The content from that template will be output into your layout _through_ this tag.

`{{ content_for }}` on the other hand accepts any content you feed it and can be placed anywhere in your Layout. It has nothing to do with the CleanSlate UI and will only output content you specify in your template's code. Think of it as a more flexible `{{ __TEMPLATE_CONTENT__ }}` tag that you feed code to in your templates.

To learn more about this, read [What are Layouts & r:yield?](https://cleanslatecms.wvu.edu/how-to/theme-development/getting-started-guide/what-are-layouts-and-r-yield) and [yielding content to other places within the DOM and Layout](https://cleanslatecms.wvu.edu/how-to/theme-development/yield-content-to-other-places).
