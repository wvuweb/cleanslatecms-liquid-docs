# Specifying Options for Custom Page Data

Again, in Liquid, this process is nearly identical. The only difference is how you incorporate custom data into your templates.

## Examples of how you might use Custom Data:

Here are a few ideas:

  * To show or hide a section of a page on your site.
    * Imagine you are redesigning a site and, over time, the content authors want to "enable" features on a per-page basis. You could use an [`if` statement](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-if-and-r-if-not) and have Custom Data with a `Yes` or `No` radio choice to show or hide this feature. The code might look like this:

```
{% if page.data.show_awesome_feature == "Yes" %}
   <p>If you click "Yes" in Page Properties > Custom Data, this content will show up.</p>
{% endif %}
```

Then, your template's frontmatter would look like this:

```
---
layout: default
custom_data_attributes:
  - show_awesome_feature:
    type: radio
    title: "Show the awesome feature?"
    options:
      - "Yes"
      - "No"
    default:
      - "No"
---
```

  * Maybe you need to capture a specific string, but don't want to force users to enter the exact string.
    * For example, imagine you want to capture `wvu-triptych`, `wvu-diptych` or `wvu-media-object`. It'd be a tough sell to get a content author to remember those; however, with Custom Data, we can throw those strings into a select box so it's easy for them to choose one.

```
---
layout: default
custom_data_attributes:
  - pattern_name:
    type: select
    title: "What pattern do you want to display?"
    description: "This pattern will show up in slot_01."
    options:
      - [wvu-triptych, 1]
      - [wvu-diptych, 2]
      - [wvu-media-object, 3]
    include_blank: false
    default: 1
---
```

  * Then, your template could consume this data via `{{ page.data.pattern_name }}`.
