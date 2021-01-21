# Conditional Logic & Loops

TODO:

  * Change CSTDTS YouTube videos (2!) from the Radius versions to Liquid (when they get made).
  * Update "Tag Documentation" links in Radius docs to be unique (#a11y)

Templates can be pretty powerful. They give you the ability to make your site dynamic, allowing what is displayed to change based upon user interaction, content, and other factors.

## Conditional Logic

There may be instances where you want to display a block of content within a template only if certain conditions are met or not met. This is where `{% if %}` and `{% unless %}` come in handy. These tags work by taking two inputs and comparing them using a given operator. If the comparison is true, `{% if %}` will render its block of content. If you would like to display the block of content when the comparison is false, you would use `{% unless %}` or the [doesn't equal (`!=`) operator](https://shopify.github.io/liquid/basics/operators/).

For example, let's say you want to display a block of content only if the name of the current page is named "Special":

```
{% if page.name == "Special" %}
  This is a special page!!!
{% endif %}
```

Now suppose we only want to show a piece of content between a very specific time frame each day:

```
{% assign now = 'now' | to_time %}
{% assign t1 = '8:00 AM' | to_time %}
{% assign t2 = '5:00 PM' | to_time %}
{% if now > t1 and now < t2 %}
  <strong>Displayed between 8 AM and 5 PM daily.</strong>
{% else %}
```

Notice that, in the example above, we set `| to_time` in the variables via `assign`. This tells the system to treat the values being compared as dates instead of strings. If the values should be treated as numbers, you would need to specify `| floor`.

Also keep in mind, for the time based example above, that the system may cache page content for a short time, typically around 10-15 minutes, so you may not see the expected result immediately.

**NOTE:** Variable names in `{% if %}` statements must not contain minus (`-`) characters. Replace minus characters with underscores (`_`) or camelCase variable names to avoid unintended math operations.

### Complex control flow operators

Unlike Radius, Liquid supports complex control flow operators like:

  * `if`
  * `else`
  * `elseif`
  * `unless`
  * `case`
  * `when`

These can come in handy and simplify your control flow compared to doing the same operations in Radius. For example:

```
{% if page.name == "Bears" %}
  We love bears!
{% else %}
  No bears here.
{% endif %}
```

Read the [Tag Documentation for Conditional Logic](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-if-and-r-if-not) on this site or go to the [official Liquid documentation for control flow](https://shopify.github.io/liquid/tags/control-flow/) for more information.

## Loops

If you have a block of content that you need to repeat several times, loops can be used instead of manually copying & pasting repeatedly. You can loop over a list of items, given by a delimited string, a range of integers, or a set number of iterations. The items to be looped over can come from various places, such as page content, page attributes, custom page attributes, or even the URL.

```
{% assign items = "foo,bar,baz" | split: "," %}
<p>Item Count: {{ items.size }}</p>
{% for item in items %}
   <p>{{ item }} {{ forloop.index }}</p>
{% endfor %}
```

Read the [Tag Documentation for Loops](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-loop) or see what [attributes/methods](https://shopify.dev/docs/themes/liquid/reference/objects/for-loops) are available inside the `forloop` object.
