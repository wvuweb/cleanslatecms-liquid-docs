#### Iteration

Liquid allows you to iterate through a series of items and format them according to the markup you've specified within the r:each tag. These items can be pages, files, or blog posts.

The official Liquid documentation has [several examples of iteration](https://shopify.github.io/liquid/tags/iteration/). You can iterate with:

  * `for`
  * `for` (with parameters)
  * `cycle`
  * `cycle` (with parameters)
  * `tablerow`
  * `tablerow` (with parameters)

View the official documentation to see examples of each type of iteration.

### Examples:

Iterate through blog posts:

```
{% assign articles = blog.articles %}
{% for article in articles.all %}
  <h2>{{ article.name }}</h2>
{% endfor %}
```

Iterate through pages:

```
{% assign pages = site.pages %}
<ul>
  {% for page in pages.all %}
    <li>
      <a href="{{ page.url }}">{{ page.name }}</a>
    </li>
  {% endfor %}
</ul>
```

Iterate through files/images for a lightbox gallery:

```
{% capture gallerypage %}{{ page.slug }}-gallery{% endcapture %}
{% assign images = site.files | filter_files: tags: gallerypage, types: "image" %}
<ul>
  {% for image in images.all %}
    <li class="col-md-4 col-lg-3 mb-3">
      <a href="{{ image | image_url: size: "960x640" }}" title="{{ image.description }}">
        <img src="{{ image | image_url: size: "480x320" }}" alt="{{ image.alt_text }}" />
      </a>
    </li>
  {% endfor %}
</ul>
```
