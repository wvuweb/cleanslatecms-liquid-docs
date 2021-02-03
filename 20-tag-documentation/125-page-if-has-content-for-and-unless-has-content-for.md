#### `{% if edit_mode or page.content["my_region_name"] != blank %}`

This tag allows you to check if an editable region has content.

You could similarly write a statement with [`unless`](https://shopify.github.io/liquid/tags/control-flow/#unless) to do the opposite.

### Attribute options

You must specify the name of an editable region to check via `page.content["my_region_name"]` where `my_region_name` is the name of the editable region.

### Examples

A good example for this tag is to check if there’s content in a sidebar on a page. If there’s not, don’t output the markup for the sidebar:

```
{% if edit_mode or page.content["wvu-sidebar"] != blank %}
  <aside class="sidebar">
    {% editable_region name: "wvu-sidebar" %}
  </aside>
{% endif %}
```

Another example is for student profiles. A student always has a major; however, a student doesn’t always have a minor. Here’s how to show a minor if they have one:

```
{% if edit_mode or page.content["wvu-profile__minor"] != blank %}
  <p>
    <strong>Minor: </strong>
    {% editable_region_block name: "wvu-profile__minor", type="simple" %}
      Enter the person's minor. If they don't have one, delete this text and it won't show up in production.
    {% endeditable_region_block %}
  </p>
{% endif %}
```

You could similarly use this in a loop. For example, in a profile index page, you could check if there is content in the `wvu-profile__minor` field:

```
{% comment %} First, we must get the ID of the current profile_index page, then assign it to a "pages" variable: {% endcomment %}
{% assign pages = site | get_page: page.id %}

{% comment %} Then we take the "pages" variable, get the children from that variable and assign it to a "profiles" variable which we iterate through: {% endcomment %}
{% assign profiles = pages.children %}

{% for profile in profiles.all %}
  <h2>{{ profile.content["wvu-profile__name"] }}</h2>
  {% if page.content["wvu-profile__minor"] != blank %}
    <p>{{ profile.content["wvu-profile__minor"] }}</p>
  {% endif %}
{% endfor %}
```

### FAQ

#### Why put `edit_mode` before `page.content["xyz"]`?

Short answer: performance. It's faster to check for `edit_mode` first, then check if there's content in a specific editable region versus the other way around.
