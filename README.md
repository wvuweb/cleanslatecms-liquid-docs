# CleanSlate CMS Liquid Docs

A 1:1 translation of the documentation on https://cleanslatecms.wvu.edu/how-to/theme-development from the Radius templating language to Liquid.

## How to name files

In an effort to keep files organized similarly to how they are organized on CleanSlateCMS, each file name starts with a number divisible by 5. For example, `05-page-name-here.md`. Each file must start with a number like `05, 10, 15, 20, ...` followed by the name.

If content is inside a folder, restart numbering at `05`.

If the folder has more than 19 child pages (eg: `95-page-name-here.md`), use a three digit prefix (eg: `095-page-name-here.md`).

## What is `index.md`?

Some pages are parent pages with a bunch of child pages. In this repository, they're labeled as folders. Inside each folder is `index.md` along with it's child pages.

For example, the `20-tag-documentation` folder has an index.md file. The `index.md` page refers to the [Tag Documentation](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index) parent page.

## How to convert files to HTML

I have found that [MarkedJS](https://marked.js.org/demo/?text=&options=&version=master) does the best job translating Markdown to HTML.

Once you have the HTML, we'll be able to insert it into CleanSlate via the Edit HTML button.

## What about long code blocks?

Long code blocks should use the [wvuwebgist](https://gist.github.com/wvuwebgist) Github account.
