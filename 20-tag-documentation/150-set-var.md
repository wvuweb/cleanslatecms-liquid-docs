#### `{% assign %}` & `{% capture %}`

This tag is used to set a variable.

The official Liquid documentation has a page dedicated to [variables](https://shopify.github.io/liquid/tags/variable/).

### Filter options

`pluralize` - Takes a string and makes it singular or plural tense. Eg: test/tests, rule/rules, regular/irregular.

`css_background_image` - A filter to output a string as a background image, eg: `background-image: url(https://example.wvu.edu/files/24271fb1-0561-4e5d-a750-0c0fdb44985d/1780x1780?cb=1614116587)`. 

`to_boolean` - Converts a string to a boolean value (`true` or `false`).

`to_time` - Converts a string to a valid time using the [Chronic](https://github.com/mojombo/chronic) library. See the docs for `date_format` for more information.

`date_iso8601` - Outputs a date in ISO 8601 format, eg: `2018-05-09T18:02:37-04:00`.

`date_rfc2822` - Outputs a date in Internet Message Format, eg: `Wed, 09 May 2018 18:02:37 -0400`.

`parse_json` - Parses JSON from an API. Pass the value the URL of your JSON endpoint.

`escape_xml` - Converts XML/HTML to HTML entities by removing traces of offending characters that could be wrongfully interpreted as markup.

`cdata_wrap` - Wraps the variable in `<![CDATA[ content goes here ]]` tags.

`web_request` - Accepts a URL to scrape HTML from. Returns the entirety of the HTML document.

`select_html` - See docs for [`select_html`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-select-html).

`select_html_attr` - See docs for [`select_html`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-select-html).

Liquid has a number of filters available to variables. To see a complete list, view the [official Liquid documentation](https://shopify.github.io/liquid/basics/introduction/#filters).

### Examples

How to create a variable called `my_special_page_name`:

```
{% assign my_special_page_name = page.name %}
```

Create a variable with a filter:

```
{% assign showPartial = "Yes" | to_boolean %}
```

Create a variable from custom page data:

```
{% assign showPartial = page.data.show_hero | to_boolean %}
```

You can also set variables using the `capture` tag:

```
{% capture gallerylabel %}{{ page.slug }}-gallery{% endcapture %}
```

`capture` works best when you have complex or multiline strings that need to be assigned to a variable.

Here's a multiline example using capture:

```
{% capture link_text %}
  <span class="sr-only">: {{ page.name }}</span>
{% endcapture %}

<!-- Then, use it: -->

{{ link_text }}
```

Here's how to get two different background images using `css_background_image`:

```
{% liquid
  assign background_image_small = site | first_random_image_tagged_with: label: "backpage-1-thumbnail" | image_url: size: "1780x580" | css_background_image
  assign background_image_large = site | first_random_image_tagged_with: label: "backpage-1-thumbnail" | image_url: size: "1780x1780" | css_background_image
%}
<!-- Then, use it: -->
<div style="{{ background_image_small }}"></div>
<div style="{{ background_image_large }}"></div>

<!-- Outputs: -->
<div style="background-image: url(https://example.wvu.edu/files/24271fb1-0561-4e5d-a750-0c0fdb44985d/1780x580?cb=1614116587)"></div>
<div style="background-image: url(https://example.wvu.edu/files/24271fb1-0561-4e5d-a750-0c0fdb44985d/1780x1780?cb=1614116587)"></div>
```

Please note: `capture` will not only capture the characters inside it, but also the spaces. This means these spaces will be part of your variable. You may consider using a filter like [`strip`](https://shopify.github.io/liquid/filters/strip/) to remove spaces depending on your use case. Another way to handle this would be to use [whitespace control](https://shopify.github.io/liquid/basics/whitespace/).

The official Liquid documentation has a whole section dedicated to the [`capture` tag](https://shopify.github.io/liquid/tags/variable/#capture).
