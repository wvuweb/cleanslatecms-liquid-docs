#### `{{ var | default: "Hello" }}`

This pulls the first non-blank attribute from a CleanSlate object, in the order from left to right.

### Example

```
{{ page.title | default: page.name }}
```

In the example, this says if `{{ page.title }}` attribute exists, use it. Otherwise, use  `{{ page.name }}`. This depends on what information the user has entered into the CleanSlate Page Properties modal.

You can also chain multiple `| default:` statements:

```
{{ page.title | default: page.created_at | default: page.name }}
```

This checks for a page title, then, if that doesn't exist, checks for when the page was created, then, if that doesn't exist, outputs the page's name.
