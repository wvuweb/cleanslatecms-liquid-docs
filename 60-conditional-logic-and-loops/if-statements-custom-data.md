# If statements with Custom Page Data

TODO:

  * When converting to HTML and pasting into Mercury, ensure the proper formatting of the ordered list (specifically, the code blocks).

Combining `if` statements with [Custom Page Data](https://cleanslatecms.wvu.edu/how-to/theme-development/custom-data) can yield powerful results. This how-to covers the following topics:

  * `if` statements
  * Variables
  * Custom Page Data

If you’re not familiar with those concepts, please refer to their respective pages before proceeding.

## What can you do with r:if statements and Custom Data?

The possibilities here are endless. In this tutorial, we’re going to show how to use Custom Page Data to **show and hide content** via `if` statements. We do this by using a variable for one or more of the values we're checking. Remember, variables can automagically be set and changed via Custom Page Data as they’re hoisted up to the page scope.

### Step by step:

  1. First, you need to add a Custom Page Data Attribute to your template’s frontmatter OR to your site’s `config.yml` file. We’ll use a page template for this example:

```
---
layout: default
custom_data_attributes:
  - showPartial
---
```

  1. Now that we’ve added the Custom Data Attribute, it will show up in Page Properties > Custom Data. We can add an `if` statement that checks the value of `showPartial`:

```
{% comment %}
  <!-- NOTE: If `showPartial` is true, show what's inside the if statement: -->
{% endcomment %}
{% if page.data.showPartial == "true" %}
  {% render "breadcrumbs" %}
{% endif %}
```

  1. Now that we’ve set up our Custom Page Data Attribute and our `if` statement, we can add a value to a page using our template via Pages > Page Properties > Custom Data > `showPartial`. Type `true` in this field to show the Breadcrumbs partial.

**NOTE:** We recommend adding a comment above your `if` statements to make things more human readable. `if` statements can get complicated and having an explanation is helpful.

**NOTE 2:** To make showing and hiding this content even easier for content authors, consider [specifying options](https://cleanslatecms.wvu.edu/how-to/theme-development/custom-data/options) for your Custom Page Data Attributes. This will allow content creators to, for example, use a radio input with “Yes” and “No” instead of having to write `true` or `false` inside a text input.

## `if` statement recipes:

The following recipes assume you’ve already created a Custom Page Data Attribute just as you did in Step 1 above.

### Hide by default:

See example above. Use this to add content to a page **only** if someone has explicitly set a Custom Page Data Attribute to `true`.

This can be useful if you’re working on a site in production where you want certain pages to “opt-in” to this functionality. Pages without a value for your Custom Page Data Attribute will not change.

## Show by default:

This will show the content inside the `if` statement as long as the Custom Page Data Attribute does _not_ equal true.

```
{% comment %}
  <!-- NOTE: If there is ANY VALUE other than true (including no value at all), show what's inside the r:if: -->
{% endcomment %}
{% if page.data.hidePartial != "true" %}
  {% render "breadcrumbs" %}
{% endif %}
```
