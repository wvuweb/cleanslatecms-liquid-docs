# Get a random image, file, or blog article

TODO:

  * Make note on Radius page content about cache after 1st paragraph.

It’s possible to have CleanSlate generate a random image, file, or blog article. This can be useful for changing background images on a hero element, getting a random blog post to display on your site’s homepage, or for getting a random page from within your site. CleanSlate will generate a new random image, file, or blog article every 30 seconds.

**NOTE:** While CleanSlate will generate a random image, file or article every 30 seconds, most often [the cache](https://cleanslatecms.wvu.edu/how-to/content-publishing/basic-editing/editing-content/cache) "catches" the page and will serve up the same item until the cache refreshes (about every 10 minutes). If you want true random item functionality, use JavaScript.

## Get a random image based on a label:

As an image tag in HTML:

```
{% assign randomImage = site | first_random_image_tagged_with: label: "backpage-1-thumbnail", limit: 1, types: "image", random: true %}
{% assign randomImage_url = randomImage | image_url: size: "1200x630" %}
<img src="{{ randomImage_url }}" alt="{{ randomImage.alt_text }}">
```

…Or inline as a random background image on a `div`:

```
{% assign bgStyler = "backpage-1-thumbnail" | background_styler %}
<div class="my-div" {{ bgStyler }}>
  <p>Hello world!</p>
</div>
```

The default dimensions for this image are 1720x1720.

You can also do this in a [style attribute in the head](https://gist.github.com/wvuwebgist/cc5cb00847eb166f5346f3c79be7fb73) and even have CleanSlate [generate different sizes of the image from a loop](https://gist.github.com/wvuwebgist/f118396cdac8cff76c624a53e9282172).

## Get a random blog post

```
{% assign blog = site | get_page: 123 %} <!-- Change this ID to your blog_index page's ID -->
{% assign articles = blog.articles | filter_articles: limit: 2, random: true %}
{% for article in articles.all %}
  <p>{{ article.name }}</p>
{% endfor %}
```

## Get a random page

```
{% assign pages = site.pages | filter_pages: limit: 1, random: true %}
{% for page in pages.all %}
  {{ page.name }}
{% endfor %}
```
