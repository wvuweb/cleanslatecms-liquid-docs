# Partials

TODO:

  * Change CSTDTS YouTube video from the Radius version to Liquid (when it gets made).
  * Fix link to "`render` in the Tag index" to use the Liquid version.

<div class="u-embed-container">
  <iframe title="CleanSlate Theme Development Tutorial Series #13: Partials" src="https://www.youtube-nocookie.com/embed/Y_iig89O9fQ" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen=""></iframe>
</div>

## Include a partial in your theme:

Partials allow you to modularize your code into different files. To include a partial, insert this line of code into your CleanSlate theme:

```
{% render "my-partial-name" %}
```

Replace `my-partial-name` with the name of your partial.

**Note:** Partial file names **must start with an underscore**. For example, the full filename from above would be `_my-partial-name.html`. This allows us to quickly differentiate between partials and page templates.

**NOTE 2:** When working with partials in Liquid, the path is always relative to the `views` folder--not the folder where the partial was called (like in Radius).

So, if you called a partial living in `views/layouts` and it was called `_header.html`, you'd call it like so in a template:

```
{% render "layouts/header" %}
```

See an example of partials in use in [`default.html` in the CleanSlate Toolkit](https://github.com/wvuweb/cleanslate-toolkit/blob/liquid/views/layouts/default.html) or check out [`render` in the Tag Index](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-partial).


## Shared Partials

In CleanSlate, there's a concept of "Shared Partials". Shared partials allow us to share bits of HTML from a different theme. For example, WVU's masthead and footer get served from a shared partial. We don't want to duplicate this HTML for every single site, so we serve it from one shared repository called [Code](https://bitbucket.org/wvudigital/code-liquid/src/master/).

Shared partials come in handy for colleges or departments that have things like global navigations or other shared elements that are globally used across each site within the college or department. Shared partials can be used from any repository in CleanSlate. If you would like to request a shared repository, please fill out the [site request form](https://cleanslatecms.wvu.edu/how-to/theme-development/getting-started-guide/request) and indicate the repository will be a shared repository under "Additional Comments" at the end of the form. If you foresee your college or department needing shared partials, it's a good idea to get this set up early.

**How do you use them? Glad you asked:**

Unlike shared partials in Radius, shared partials in Liquid require no additional syntax in the `render` call. The syntax is identical.

There is one thing you must do to make your theme "aware" of shared partials.

In your theme's `config.yml` file, we must tell our theme what other themes are available. Do that via the `import_themes:` key:

```
import_themes:
  - git@bitbucket.org:wvudigital/code-liquid.git
  - git@bitbucket.org:wvudigital/example-theme-name-that-you-should-change.git
```

You can find this path by clicking "Clone" in Bitbucket and copying _part_ of the provided text.

Once you define your shared themes in `config.yml`, you can call any partial in that theme just like you did above.

## FAQ:

### There's a "views" and a "layouts" folder. Where do I save partials?

Great question! Partials can be saved anywhere within your `views` folder. You can create sub-folders to house your partials and reference them via the path in your `render` tag (as noted above).

Generally speaking, partials in many themes live in a sub-folder of `views`, usually something like `custom-patterns` or `components`. The folder can be called anything you like (eg: `giraffe`!). This is not required by the system--it's just an understood design pattern that has emerged over the years.
