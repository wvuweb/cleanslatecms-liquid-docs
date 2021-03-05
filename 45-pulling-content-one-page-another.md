# Pulling content from one page to another

TODO:

  * Change CSTDTS YouTube video from the Radius version to Liquid (when it gets made) & include video label.
  * Insert Gists as noted below (see **NOTE:**'s)

In CleanSlate, it’s possible to have content live on one page of your site and pull that content to other parts of your site.

A common use case for this are Blog Index and Profile Index templates. On a Profile Index template, you are going to have a person’s name, profile photo and a link to their full biography.

It would be a pain to copy that content into a different place on your site if it already exists elsewhere. Luckily, we can programmatically pull this content from one page to another.

For this example, let’s build the following profile templates: `profile_individual.html` and `profile_index.html`.

First, `profile_individual.html`.

In our Profile Individual template, we need the following editable regions for each person’s page:

  * Name
  * Profile Photo
  * Job Title
  * Phone Number
  * Email
  * Biography excerpt (for the profile index)
  * Full Biography

Let’s see what that looks like in code. Here’s a profile_individual.html template:

**NOTE:** Insert profile_individual_liquid.html Gist here using the Gist snippet: https://gist.github.com/wvuwebgist/acd998c58c274089a0b8dc293338ec8d

## Understanding how to pull content from one page to another

In CleanSlate, if content lives on a page in an editable region, you can target that page to pull content from that page’s editable regions. This is achieved by using [a loop](https://cleanslatecms.wvu.edu/how-to/theme-development/conditional-logic-loops) and one or two of the following tags/drops:

  * `pages.children`
  * `pages.descendants`
  * `blog.articles`
  * `get_page`

Using `pages.children` means you will be looping through a series of child pages in your site map. For example, imagine we have pages with the following structure:

  * Faculty
    * Sarah Jane
    * Jeff Murphy
    * Rodrigo Smith
  * Staff
    * Wesley Kee
    * Zoe Gillipspe
    * Sally Mejia

If we wanted to use `pages.children`, we’d assign the “Faculty” and “Staff” pages the `profile_index.html` template. That template would output the three people under each page, respectively. Here’s how that might look:

**NOTE:** Insert profile_index--simple-liquid.html Gist here using the Gist snippet: https://gist.github.com/wvuwebgist/1dada3127dad5ac1d317d6b2841971fe

## `profile.content` does all the heavy lifting

When pulling content from one page to another, `profile.content` (and `article.content`, for that matter) do all the heavy lifting:

```
{{ profile.content['wvu-profile__name'] }}
```

This tag is searching the page for an [editable region](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-editable-region) with the name `wvu-profile__name` and pulling all of the content from within that editable region, then outputting it on our template.

One thing to note: `page.content` and `article.content` are functionally identical; however, `article.content` must be used on a blog. Also, both must be used within a loop. In other words, most of the time you will use these tags within one of the following tags:

  * `pages.children`
  * `pages.descendants`
  * `blog.articles`
  * `get_page`

## Putting together our `profile_index.html` template

Now that we’ve talked about `page.content`, let’s look at what a profile index template would look like:

**NOTE:** Insert `profile_index.html` Gist here using the Gist snippet: https://gist.github.com/wvuwebgist/fd94d14a4811e0a0d616d8663d528eb7

As you can see, this template pulls content from the following editable regions of each child page:

  * Profile Photo
  * Name
  * Job Title
  * Phone Number
  * Email Address
  * Short Description / Biography

To see how this might look, check out the profile templates in the [Brand Patterns theme](https://github.com/wvuweb/brand-patterns/tree/master/views) and the [example pattern](https://patterns.wvu.edu/patterns#wvu-profile-page-examples) on its website.

**NOTE:** This technique works with content on the **same site**. You cannot use `profile.content` to pull content from one site into another site. If you're looking to share profiles across sites, you should look into using XSLT, the `web_request` tag, or create a JSON API in the host site and consume that API with JavaScript on the source site. Contact [CleanSlate@mail.wvu.edu](mailto:cleanslate@mail.wvu.edu) for more information.

**NOTE 2:** Don’t want to pull _all_ the content from an editable region? Limit what is pulled with the `select_html` filter:

```
{{ profile.content['wvu-profile__short-description'] | select_html: css_selector: 'p', limit: 2 }}
```
