# Yielding content to other places within the DOM & Layout

TODO:

  * Change CSTDTS YouTube video from the Radius version to Liquid (when it gets made).
  * Update grammar of first sentence in Radius docs.
  * Change `page-js` to `page_js` in Radius docs.
  * Update grammar/punctuation/cadence of last two paragraphs on Radius docs to match what's here.

Sometimes you may want to place certain things in different places than where your normal `{{ __TEMPLATE_CONTENT__ }}` tag is. For example: you may want to move JavaScript to just before your closing `</body>` tag. Or, you want to put another stylesheet in your `<head>` but you only want this CSS or JavaScript to be used in one specific template (eg: `frontpage.html`).

To do that, place:

```
{{ content_for.page_js }}
```

into your layout (probably `default.html`) where you want the content to appear. This is your "hook." Then, in your template (say `frontpage.html` for example), place:

```
{% content_for "page_js" %}
  <!-- Your stuff goes between these tags! -->
{% endcontent_for %}
```

In this example, I called it `page_js`. You can name it whatever you want (as long as you follow the [best practices](http://cleanslatecms.wvu.edu/how-to/theme-development/getting-started/convert-theme#making-an-editable-region) outlined on the [Convert a theme to CleanSlate page](https://cleanslatecms.wvu.edu/how-to/theme-development/getting-started-guide/convert-theme)).

You want to be sure to include the same name in both places (e.g., in your layout [say `default.html`] and in your page template [say `frontpage.html`]). In other words, don't just copy and paste blindly, rename `page_js` to what you want it to be! The [DIY Outdoors theme](https://bitbucket.org/wvudigital/diyoutdoors/src/1641169f20d4cda9468e3c969b76efb25c81e6ae/views/backpage_map.html#lines-38) has a good example of this technique.