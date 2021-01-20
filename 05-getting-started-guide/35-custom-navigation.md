# Custom Navigation

TODO:

  * Change CSTDTS YouTube video from the Radius version to Liquid (when it gets made).

In CleanSlate, there are currently five different ways to create navigation.

  1. **`{% site_menu %}`:** This tag outputs your navigation starting from your site's root. There are several attributes you can add to this tag. [View the `site_menu` documentation in the tag index](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-site-menu).

  1. **`{% sub_menu %}`:** The sub menu tag lists the child pages that are direct descendants of the current page as an unordered list. It also accepts a number of attributes. [View the `sub_menu` documentation in the tag index](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-sub-menu).

  1. **`{% ancestor_menu %}`:** This will list all pages going up from the current page and pages at the root. So, if you put this tag in a page nested deep within your site, it will print out all pages above and below the current page. It will not print out pages nested beneath other root level pages. The menu to the right is an example of the ancestor menu. Again, read up on the documentation for [`ancestor_menu` on its page in the tag index](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-ancestor-menu).

  1. **Use labels on pages to make a custom navigation.** Log in to CleanSlate, go to your site > Pages. Select the pages you want to include in the navigation and add a label to them. Then, in your template, follow these instructions to generate a [Page Label Menu](https://cleanslatecms.wvu.edu/how-to/theme-development/page-label-menu).

  1. **Make it manually with `data-page-id` attributes:** You can always create an unordered list manually. As an added bonus, you can use a `data-page-id` attribute to dynamically generate the URL in the `href` field. This makes sure that, if the permalink or page name changes, the link does not break. A page always has one ID and it never changes. The [DIY Outdoors](https://diyoutdoors.wvu.edu/) site uses this for their activity and main navigation. View the [activity navigation](https://bitbucket.org/wvudigital/diyoutdoors-v2/src/master/views/custom-patterns/_activity-nav__list.html) and [main navigation](https://bitbucket.org/wvudigital/diyoutdoors-v2/src/master/views/custom-patterns/_diy-main-navigation.html) code.
    * **Example:** `<a href="path/to/my/page" data-page-id="1234">Example Link</a>`
    * **How do I find a page's ID?** Log in to CleanSlate and edit the page you want to link to. In your browser's URL bar, you'll see: `https://cleanslate.wvu.edu/sites/13/pages/3618/editor`. In this case, 3618 is that page's ID.
    * As an added bonus, you'll notice when you make a link to a page inside your site in the editor, the system will add a `data-page-id` attribute to each link.
