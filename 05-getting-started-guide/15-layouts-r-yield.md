# What are "layouts" and "r:yield"?

TODO:

  * Change CSTDTS YouTube video from the Radius version to Liquid (when it gets made).
  * Should we rename this page to, "...'layouts', 'r:yield' and 'TEMPLATE_CONTENT'"?"

Layouts are a new way of organizing your theme. The concept was born from the structure of [Rails](http://rubyonrails.org/) applications. The goal is to modularize your code and keep it DRY'er.

To better understand the layouts concept, let's examine [Slate themes are structured](https://github.com/wvuweb/slate-toolkit/tree/master/default-theme/html5_rhtml).

In Slate, we split up partials with a `_header.rhtml`, `_masthead.rhtml`, `_navigation.rhtml`, and `index.rhtml`/ `backpage.rhtml`. `_header.rhtml` houses most of our code for our `<head>`. Often, our `_header.rhtml` file would open the `<head>` tag, but not close it. This can lead to questions like, "Where is the closing `<head>` tag? Why don't tags open and close in the same file?"

## Enter layouts.

Layouts allow us to have a central place to open and close tags and keep everything modularized in one file. Layouts allow the flexibility to include partials (other modularized bits of code) and _yield_ content into other parts of the document where we see fit.

### What is `{{ __TEMPLATE_CONTENT__ }}`?

`{{ __TEMPLATE_CONTENT__ }}` is where a template gets rendered and inserted into your document. For example, all the code in `backpage.html` will be inserted wherever your `{{ __TEMPLATE_CONTENT__ }}` tag is.

### How is `{{ __TEMPLATE_CONTENT__ }}` different than a partial?

`{{ __TEMPLATE_CONTENT__ }}` allows you to select a template—like `Backpage` or `Frontpage`—to use through the UI.

In contrast, a partial only grabs a unique file containing a single set of code.

### Can I see an example?

Sure! Check out [default.html in the CleanSlate Toolkit](https://github.com/wvuweb/cleanslate-toolkit/blob/liquid/views/layouts/default.html).

Note the `{{ __TEMPLATE_CONTENT__ }}` tag. Now check out the [`backpage.html` template](https://github.com/wvuweb/cleanslate-toolkit/blob/liquid/views/backpage.html). This `backpage.html` template defines a layout at the top of the file (`layout: default`, around line 2). From this, we know that the contents of `backpage.html` will be yielded into [`default.html`](https://github.com/wvuweb/cleanslate-toolkit/blob/liquid/views/layouts/default.html), where the `{{ __TEMPLATE_CONTENT__ }}` tag is (around line 30).

At the end of the day, layouts are just a different approach to making themes. Layouts will make more sense to you after you build a couple themes. My guess is, after you have familiarized yourself with the concept, you'll enjoy the structure. You'll also notice how much less repeated code exists between templates (`backpage.html`, for example) using layouts.
