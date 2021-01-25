#### `{% link_javascript %}`

JavaScript must be stored in a directory called `javascripts`. To include a file called `main.js`, use this syntax:

```
{% link_javascript name: "main" %}
```

Do not include the `.js` extension when adding file names.

You can also include multiple scripts by separating them with commas. For example, if you wanted to add three files named `file-1.min.js`, `file-2.min.js`, and `file-3.js`, add them like so:

```
{% link_javascript name: "file-1.min, file-2.min, file-3" %}
```

## Attribute Options

`async` - Boolean value (`true` or `false`). Used to load javascript asynchronously.

`defer` - Boolean value (`true` or `false`). Used to defer loading javascript until other resources have been loaded.

## Example:

```
{% link_javascript name: "file-1.min, file-3", async: false, defer: false %}
```

**NOTE:** Don't use async and defer on the same `link_javascript` tag. This is [an antipattern](https://twitter.com/csswizardry/status/1331721659498319873).

## Notes on ES6

CleanSlate uses the [Uglifier gem](https://github.com/lautis/uglifier) to mangle and minify JavaScript resources. If your JavaScript file won't load or you get the message, "Holy moly, we just blew a fuse.", you should check to make sure:

  * The name and path to the file are correct.
  * The file doesn't have any JavaScript that uses [ES6](https://www.quora.com/What-is-ES6?share=1) syntax.

At this time, CleanSlate will not load or parse ES6. If you want to use ES6, transpile your JavaScript before including it in CleanSlate via a tool like [Babel](http://babeljs.io/).
