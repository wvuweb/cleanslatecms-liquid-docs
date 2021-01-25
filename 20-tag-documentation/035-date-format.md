#### `{{ page.published_at | date: '%A, %B %d, %Y' }}`

This outputs a date. It can be used to pull the date from when a [blog post](https://github.com/wvuweb/cleanslate-toolkit/blob/liquid/views/blog_article.html#L17) or page was published, output the time, day, and/or year on page render. It has many other uses.

In Liquid, you access the native date via `{{ page.published_at }}` or `{{ article.published_at }}`, then pipe in the [date filter](https://shopify.github.io/liquid/filters/date/) to output the date in the format you desire.

Under the hood, CleanSlate uses the [Chronic](https://github.com/mojombo/chronic) library to parse the original value. So, any date/time value supported by Chronic can be parsed.

### Filter options

`date` - Tells the tag how to output the date. For example: `11/01/14` or `November 1, 2014`. Acceptable values come from [strftime](http://strftime.net/).

`date_iso8601` - Outputs a date in ISO 8601 format, eg: `2018-05-09T18:02:37-04:00`.

`date_rfc2822` - Outputs a date in Internet Message Format, eg: `Wed, 09 May 2018 18:02:37 -0400`.

### Examples:

```
{{ page.published_at | date: '%A, %B %d, %Y' }}
<!-- Outputs: Wednesday, May 09, 2018 -->
```

```
{{ article.published_at | date: '%Y' }}
<!-- Outputs: 2021 -->
```

```
{{ page.updated_at | date_rfc2822 }}
<!-- Outputs: Wed, 09 May 2018 18:02:37 -0400 -->
```

```
This page was last updated at {{ "now" | date: "%Y-%m-%d %H:%M" }}.
<!-- Outputs: This page was last updated at 2019-09-19 17:48. -->
```
