#### `page.{attr}`

TODO:

  * Attributes that don't exist yet: `link_class`, `link_target`, `link_title`, `link_value`(?)
    * TODO: AJ test these attributes after Nathan pushes.
  * `is_home_page?` doesn't return true or false when used with an object (`{{ page.is_home_page? }}`). Should it?

Use this tag to get properties about the current page (or current page in a loop), where `{attr}` is replaced by one of the attributes listed below.

### Attribute options

  * `id` - Get the page ID. Returns a number. (eg: `12345`)
  * `name` - Get the page name.
  * `slug` - Get the slug of the current page (eg: `my-page-slug-from-the-url`).
  * `url` - Get the URL of the current page (eg: `https://example.wvu.edu/backpage-1`).
  * `editor_url` - The the URL for the current page in edit mode (eg: `http://cleanslate.wvu.edu/sites/223/pages/45/editor`)
  * `meta_description` - Get the meta description of the current page (Page Properties > Description).
  * `title` - Get the page title.
  * `alternate_name` - Get the alternate name as listed in Page Properties.
  * `depth` - The depth of the page relative to the root level. Numbering starts at `1`.
  * `previous_sibling` - The previous sibling page.
  * `next_sibling` - The next sibling page.
  * `parent` - Access the parent page's properties (eg: `{{ page.parent.name }}`).
  * `created_at` - The date the page was created (eg: `2018-05-09 18:02:22 -0400`)
  * `updated_at` - The time when the page was last updated either via content or page properties. (eg: `2021-02-10 15:29:42 -0500`)
  * `content_updated_at` - The time when the content on the page was last updated (eg: `2021-01-29 16:43:10 -0500`)
  * `published_at` - The time when the page was first published (eg: `2018-05-09 18:02:37 -0400`)
  * `template_name` - The name of the page's template as seen in page properties.
  * `author` - Returns an object containing information about the page author. Use: `page.author.full_name`, `page.author.first_name` and `page.author.last_name`.
  * `content` - Used to get the content from an editable region. Use: `page.content["main"]` where "main" is the name of the editable region you want to reference. Can also be used in a loop.
  * `tags` - The labels/tags associated with a page. Multiple labels/tags return as a comma separated list without spaces (eg: `a-label,featured,test-bears-label`)
  * `tags_match` - Specify `any`, `all` or `none` as to how to match which of the referenced labels. `any` means any page with any one of the labels. `all` means the page must have every label specified in the list. `none` means pages that _don't_ have the specified labels.
  * `data` - Gets the [Custom Page Data](https://cleanslatecms.wvu.edu/how-to/theme-development/custom-data) associated with the current page. (eg: `page.data.show_awesome_feature` or `page.data["show_awesome_feature"]`)
  * `data_saved?` - Checks if custom page data has ever been saved/set for the current page. Often [used with `unless` to assign values to variables](https://bitbucket.org/wvudigital/ur-apartments/src/d66cab71c12dfaf5f2bea02164a2cb6752ed58b8/views/includes/_wvu-component-footer.html#lines-3:9) if no values are present.
  * `is_home_page?` - Tests if the page is the home page. Used with `if` tags (eg: `if page.is_home_page?`)
  * `descendants` - Get all pages under the current page, no matter the level. This page drop is most often used with a loop (eg: `page.descendants` or `page.descendants.first`). Returns an array.
  * `ancestors` - This will list all pages going up from the current page and pages at the root. If you put this tag in a page nested deep within your site, it will print out all pages above and below the current page. It will not print out pages nested beneath other root level pages. This page drop is most often used with a loop. Returns an array.
  * `children` - Get all the pages directly under the current page. This page drop is most often used with a loop. Returns an array.
  * `siblings` - Get all the pages at the current level. This page drop is most often used with a loop. Returns an array.
  * `slots` - Slots are a functionality specific to something colloquially called "Super Theme". See an implementation of slots in the [UR Apartments theme](https://bitbucket.org/wvudigital/ur-apartments/src/liquid/views/utilities/_wvu-slots.html). Slots can be detrimental to your site's performance, so we recommend only using them when creating a custom template is not feasible.

Note: `<r:page:first_non_blank_attr />` has been replaced by the `default` filter. Eg: `{{ page.alternate_name | default: page.name }}`.

### Examples

Simple page drops:

```
{{ page.id }} <!-- 12345 -->
{{ page.name }} <!-- "My Test Page" -->
{{ page.url }} <!-- https://example.wvu.edu/my-test-page -->
{{ page.tags }} <!-- "abc-label,featured,hello-world" -->
```

Many of the attributes above can be used in Liquid objects (👉`{{ example }}`). For those that return objects, you oftentimes must use a loop:

```
{% assign children = page.children %}
<ul class="child-page-list">
  {% for child in children.all %} <!-- or children.first / children.last -->
    <li><a href="{{ child.url }}">{{ child.name }}</a></li>
  {% endfor %}
</ul>
```

Get a page's name based on a page ID:

```
{% assign pages = site.pages | get_page: 1234 %}
{% for page in pages.all %}
  <p>{{ page.name }}</p>
{% endfor %}
```

Get up to three sibling pages:

```
{% assign siblings = page.siblings | filter_pages: limit: 3 %}
{% for sibling in siblings.all %} <!-- or siblings.first / siblings.last -->
  <p>{{ sibling.name }}</p>
{% endfor %}
```

You can also use page drops in `if` tags:

```
{% if page.is_home_page? %}
  I'm the homepage!
{% endif %}
```

Or with [Custom Page Data](https://cleanslatecms.wvu.edu/how-to/theme-development/custom-data):

```
{% if page.data.show_awesome_feature == "Yes" %}
   <p>If you click "Yes" in Page Properties > Custom Data, this content will show up.</p>
{% endif %}
```

Or to output markup if an editable region has content in it:

```
{% if edit_mode or page.content["main"] != blank %}
  <div class="col-8">
    {% editable_region name: "main" %}
  </div> <!-- /.col-8 -->
{% endif %}
```
