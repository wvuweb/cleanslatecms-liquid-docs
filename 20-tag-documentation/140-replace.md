#### `{{ "Hello World" | replace: "Hello", "Hi" }}`

Replaces every occurrence of the first argument in a string with the second argument.

View the official Liquid documentation for the [replace filter](https://shopify.github.io/liquid/filters/replace/).

### Examples

```
{{ "Wordpress is the best CMS" | replace: "Wordpress", "CleanSlate" }}
<!-- Output: "CleanSlate is the best CMS." -->
```

```
<!-- Input: page.name = "Wordpress is the best CMS" -->
{{ page.name | replace: "Wordpress", "CleanSlate" }}
<!-- Output: "CleanSlate is the best CMS." -->
```

```
{{ "Morgantown is located in Morgantown, WV." | replace_first: "Morgantown", "WVU" }}
<!-- Output: "WVU is located in Morgantown, WV." -->
```

**Note:** Liquid does not support Regular Expressions (RegEx) due to security reasons. It does have a wide variety of [Filters](https://shopify.github.io/liquid/filters/abs/) that can likely suit your needs.
