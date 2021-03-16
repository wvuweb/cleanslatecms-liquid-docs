# Blog Templates

TODO:

  * Change CSTDTS YouTube video from the Radius version to Liquid (when it gets made).

## FAQ:

**Does CleanSlate support blogs?** Yes.

**Can you have multiple blogs on a single site?** Yes

**Do you have code examples of blog index and blog article templates?** Absolutely! Check out the [`blog_index.html`](https://github.com/wvuweb/cleanslate-toolkit/blob/liquid/views/blog_index.html) and [`blog_article.html`](https://github.com/wvuweb/cleanslate-toolkit/blob/liquid/views/blog_article.html) templates in the [CleanSlate Toolkit](https://github.com/wvuweb/cleanslate-toolkit/tree/liquid)—a boilerplate for making themes in CleanSlate.

**Can you have different templates for different blog posts?**

Yes. Say, for example, you had different authors and you wanted a bio to appear at the bottom of posts they write. Each author could have his or her own template. Another example could be a blog post that includes a YouTube video. You could have a field for the video in a `blog_article--youtube.html` template.

**How do I pull articles from my blog onto my site's homepage?**

Do this using the [blog.articles tag](https://gist.github.com/wvuwebgist/d149c22aed588af4a05407832c9e2c5d) by passing it a blog ID. Note: this pulls blog articles from the same site—not from a different site.

**How do I pull blog articles from a different site?**

Use the [RSS Feed Snippet](https://cleanslatecms.wvu.edu/how-to/content-publishing/advanced-editing/snippets/rss-snippet). You can customize your site's RSS feed output in `blog_index.rss`.

**How do I tag articles in CleanSlate?**

Tag a blog article by adding a label to it in Pages. To filter blog posts by tag(s), follow this format: `http://example.wvu.edu/blog?tags=example` where `example` is the tag and `/blog` is the permalink to your blog's homepage. Separate multiple tags with commas in the URL.

**How do I add a featured blog post to my homepage (or another page)?**

You can add a label or multiple labels to a blog post or blog posts using [this code in your template](https://gist.github.com/wvuwebgist/023a0ef7bd5617bf6cea1b1555b0ab01). First, change the blog ID. Then, choose which tag(s) you want included via `tags: "my-tag,my-tag-2"`. Choose how many posts to display via `limit: "1"`. Here's a [simplified example](https://gist.github.com/wvuwebgist/88de48f8baed233c8ab14637d3c4c834) if you're looking to break this code down.

**Can I exclude a certain label from a blog feed?**

This usually happens if you don’t want your “featured stories” repeated next to your regular blog articles. To exclude a certain label from a list of blog articles, use `tags_match: "none", tags: "dont-show-stuff-with-this-label"` on the `{% assign articles %}` tag. Here’s an [exclude label code example](https://gist.github.com/wvuwebgist/71023ca0e028f9bc879263ac8e64cb97).

**How do I pull articles from multiple tags/labels?**

Where you're referencing `tags: "xyz"`, enter your tags/labels as a comma separated list _without_ spaces. For example: `tags: "history,art,event"`.

**How do I pull blog posts that include ALL of the included labels?**

On the `{% assign articles %}` tag, include `tags_match: "all", tags: "admissions,year-2050"`. This will only show blog posts with both `admissions` and `year-2050` labels.

**Can I pull a list of blog posts onto another page, but have content authors specify which tags/labels to pull via the CleanSlate UI?**

Yes. Specify [Custom Page Data](https://cleanslatecms.wvu.edu/how-to/theme-development/custom-data) for the page where you want to pull the posts, then use `get_page` and `filter_articles` to output the list. Here is a [code example for dynamic labels via the CleanSlate UI](https://gist.github.com/wvuwebgist/29b9ba11dbede01dec7a10e5395ca30e).

**Does CleanSlate have comments for blogs?**

Not natively; however, we believe services like [Disqus](http://disqus.com/) and [many others](https://www.quora.com/Are-there-any-free-alternatives-to-Disqus) accomplish this better than we could. We have had good experiences with Disqus in the past (we're even using Disqus for comments on this site's blog!).

**I'm getting an application error for my blog. What's the deal?**

It's likely that you created your blog page as a "Content Page" instead of a "Blog Index" page. In order for a blog to work, you must create the parent page (the root of the blog) as a "Blog Index" page. You cannot switch a normal "Content Page" to be a Blog Index. Pages are different from blogs and have different functionalities.

**Wait, I thought you just said I can have any number of templates for my blog posts.**

Yup, you can. But your _blog index_ must be created as a "Blog Index" page type in Your Site > Pages > Create Page.

**Does CleanSlate support blog post thumbnails?**

You mean like [thumbnails like this](https://gwac.wvu.edu/blog)? Absolutely! You'll notice the `css_selector` attribute on your [`blog_index.html` page](https://github.com/wvuweb/cleanslate-toolkit/blob/liquid/views/blog_index.html#L25). If you want to pull more than just a paragraph, add in the other tags in a comma separated list. In this case, image and paragraph tags: `css_selector="img, p"`. You can also use a dedicated editable region for an image, then pull that into your blog index template.

**I'm redesigning a site with lots (100+) blog articles. Is there a way to move blog articles from one site to another?**

Yes, this is possible. There are a few things to keep in mind. 1) The blog's editable regions need to be the same. 2) Moving blog articles from one site to another is a "cut" operation, not a "copy". Thus, once the articles have been moved, they only exist in one place and are no longer accessible at the old domain. Keep this in mind when launching your new site. Any assets used in blog posts can be copied to the new site. Labels/tags can be copied too if specifically requested.

Moving a blog is oftentimes a tedious process, no matter how you approach it. Depending on the redesign, it may make more sense to manually migrate the content so that you can simultaneously adapt it to the new design and reformat content as necessary.

If you would like help migrating a blog, fill out the [Request Help Form](https://urwvu.wufoo.com/forms/m15c3h181kox77o/) or email [CleanSlate@mail.wvu.edu](mailto:cleanslate@mail.wvu.edu).

**I have a question you didn't cover here. Where do I get answers?**

You can either email [CleanSlate@mail.wvu.edu](mailto:cleanslate@mail.wvu.edu) or use the [Request Help Form](https://urwvu.wufoo.com/forms/m15c3h181kox77o/). We're happy to hear from you!
