# Convert a theme to CleanSlate

TODO:

  * Link to the liquid version of the "Tag Index".
  * Add note about Radius + Liquid templating languages (3rd paragraph on this page) to Radius docs.
  * NOTE: omitted the theme conversion screencast. Maybe make a new one and add it here?
  * Properly case "JavaScript" vs "javascript" in Radius docs.
  * Double check code for pulling an image in a theme's `images` directory via Liquid (`theme_image_url`) to make sure this works.
  * Update Radius docs from "sitewide" to "site wide"

CleanSlate uses a template language called [Liquid](https://shopify.github.io/liquid/). Therefore, all tags will look something like `{% my_tag %}` or `{{ my.tag }}`.

A company called Shopify created Liquid. Shopify has a number of learning resources available. One that is particularly helpful is this 28 minute [Overview of Liquid](https://www.youtube.com/watch?v=-ihFPNcSkT4) video on YouTube. While not everything will translate 100% to CleanSlate, it will give you a good understanding of the core language and how it's used. For a more in-depth description of the various tags available, visit the [Tag Index](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index).

<p style="font-size: .8rem;"><strong>NOTE:</strong> CleanSlate actually supports two templating languages: Radius and Liquid. As of 2021, Liquid has taken over as the dominant templating language because it's far more performant than Radius. The Radius templating language will be depreciated in the future. All themes moving forward should use Liquid.</p>

## It's dangerous to go alone! Take this.

After several years and hundreds upon hundreds of themes for Slate and CleanSlate, we've learned the best themes are made when you start with a boilerplate. We maintain a number of boilerplates for CleanSlate themes. One of them is called the [CleanSlate Toolkit](https://github.com/wvuweb/cleanslate-toolkit/tree/liquid). When you're starting to convert a theme to CleanSlate, use the CleanSlate Toolkit as your base and build off of it. It's very bare bones, delete key friendly and will save you time.

<p style="font-size: .8rem;"><strong>NOTE:</strong> If you're starting fresh and building a theme from scratch, we recommend starting with the <a href="https://designsystem.wvu.edu/">WVU Design System</a>, <a href="https://supertheme.sandbox.wvu.edu/">Supertheme</a> or <a href="https://patterns.wvu.edu/">Brand Patterns</a>. The CleanSlate Toolkit is a great bare bones theme—best for getting to know CleanSlate and providing simple examples—but these newer themes are actively maintained, branded, more feature rich and accessible.</p>

Without further adieu, let's see how to get your theme up and running in CleanSlate:

## Linking stylesheets:

HTML: `<link href="http://mysite.wvu.edu/stylesheets/styles.css" rel="stylesheet">`

CleanSlate: `{% link_stylesheet name: "styles" %}`

**Or, if your stylesheet is in a subfolder of your `stylesheets` directory:**

HTML: `<link href="http://mysite.wvu.edu/stylesheets/path/to/awesome/styles.css" rel="stylesheet">`

CleanSlate: `{% link_stylesheet name: "path/to/awesome/styles" %}`

**Bonus:**

You can include multiple stylesheets at once by passing a comma separated list to the `link_stylesheet` tag. Each file will be compressed (if you have it enabled in your `config.yml` file) and all files will be combined into one.

HTML:

```
<link href="http://mysite.wvu.edu/stylesheets/reset.css" rel="stylesheet">
<link href="http://mysite.wvu.edu/stylesheets/fonts.css" rel="stylesheet">
<link href="http://mysite.wvu.edu/stylesheets/styles.css" rel="stylesheet">
```

CleanSlate: `{% link_stylesheet name: "reset, fonts, styles" %}`

If you have a stylesheet in a subdirectory of stylesheets, simply include the path:

```
{% link_stylesheet name: "reset, fonts, path/to/awesome/styles" %}
```

## Linking JavaScript

HTML: `<script src="../javacripts/jquery.js"></script>`

CleanSlate: `{% link_javascript name: "jquery" %}`

**Bonus:** Much like stylesheets, you can also include multiple JavaScript files in one Liquid tag:

HTML:

```
<script src="../javacripts/jquery.js"></script>
<script src="../javacripts/jquery.backstretch.js"></script>
<script src="../javacripts/jquery.custom.js"></script>
```

CleanSlate: `{% link_javascript name: "jquery, jquery.backstretch, jquery.custom" %}`

## Linking up a stylesheet or JavaScript file from outside your theme

The syntax doesn't change here. Please note: **always link to the HTTPS resource**. You may need to change `http` to `https`.

HTML & CleanSlate: `<link href="https://mysite.wvu.edu/path/to/styles.css" rel="stylesheet">`

If the asset you're linking to doesn't exist over HTTPS, consider downloading it and hosting it from your theme.

## Linking up images inside your theme

HTML: `<img src="../images/my-image.jpg" alt="Foo bar" />`

CleanSlate: `<img src="{% theme_image_url name: "my-image.jpg" %}" alt="Foo bar">`

## Outputting your main navigation in a `<ul>`:

CleanSlate: `{% site_menu %}`

Want to add a `class` or `id` to your `<ul>`? No problem!

Class: `{% site_menu ul_class: "your-class-here" %}`

ID: `{% site_menu ul_id: "your-id-here" %}`

## Making an editable region:

CleanSlate (Radius): `<r:editable_region name="main" />`

CleanSlate (Liquid): `{% editable_region name: "main" %}`

Editable region names (`name: "xyz"`) **must not have any spaces, punctuation or upper case letters**. Additionally, each editable region name **must be unique**. No two editable regions can be named identically in the same page template (e.g., You cannot have two `name: "xyz"` in one template. Weird stuff will happen).

## Making a "simple" editable region:

In CleanSlate, you can create editable regions without WYSIWYG abilities. We call these **simple editable regions**. These regions are appropriate for titles, headlines or any area where you want just the content and not the styles.

CleanSlate (Radius): `<r:editable_region name="main" type="simple" />`

CleanSlate (Liquid): `{% editable_region name: "main", type: "simple" %}`

## Making an editable region with site wide content:

CleanSlate (Radius): `<r:editable_region name="contact" scope="site" />`

CleanSlate (Liquid): `{% editable_region name: "contact", scope: "site" %}`

If you make an editable region, then later decide to make it an editable region with global content, best practice is to give the region a **new name** in the `name: "xyz"` field to avoid confusion in the CleanSlate database (and on your pages!).

## Making an editable region with default content:

There are a few ways to do this. One with a simple string and another with whatever content and HTML you would like:

CleanSlate (Radius):

```
<r:editable_region name="main">
  My default content goes here.
</r:editable_region>
```

CleanSlate (Liquid):

```
{% editable_region name: "main", placeholder: "My default content goes here." %}
```

OR:

```
{% editable_region_block name: "main" %}
  My default content goes here.
{% endeditable_region_block %}
```

Note the difference between `editable_region` and `editable_region_block`.

## Include a partial in your theme:

CleanSlate allows you to modularize your code into partials. Partials must live somewhere inside the root `views` folder, start with an underscore and end in `.html`. Example: `_my-partial.html`.

CleanSlate (Radius): `<r:partial name="my-partial" />`

CleanSlate (Liquid): `{% render "my-partial" %}`

You can also nest partials into different folders inside the `views` folder. For example, if you had a partial at `views/custom-patterns/_my-partial.html`:

CleanSlate (Radius): `<r:partial name="custom-patterns/my-partial" />`

CleanSlate (Liquid): `{% render "custom-patterns/my-partial" %}`

For more information about partials, including learning about "Shared Partials", view the page dedicated to [Partials](https://cleanslatecms.wvu.edu/how-to/theme-development/partials).

## Outputting breadcrumbs in a `<ul>`:

CleanSlate (Radius): `<r:breadcrumbs ul_class="breadcrumbs" />`

CleanSlate (Liquid): `{% breadcrumbs ul_class: "breadcrumbs" %}`
