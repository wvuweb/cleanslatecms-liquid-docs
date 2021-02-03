#### `if`, `elsif`, `else`, `unless` and `case/when`

These tags render a block of content only if a set of conditions are or are not met.

See our documentation on [Conditional Logic and Loops](https://cleanslatecms.wvu.edu/how-to/theme-development/conditional-logic-loops) for more in-depth explanations. Also, see the official Liquid documentation on [Control Flow](https://shopify.github.io/liquid/tags/control-flow/) for more examples.

### Attribute options

In Liquid, `if` tags don't have value attributes. They compare the actual items themselves.

**NOTE:** Variable names in `if` statements must not contain dash/minus (`-`) characters. Replace dashes with underscores (`_`) or camelCase variable names.

`operator` - The operator to use to compare value1 to value2. Can be one of the following: `==`, `!=` (does not equal), `>`, `<`, `>=`, `<=`.

`or`/`and` - Use these keywords to check two different conditions simultaneously.

`contains`/`blank`/`empty` - In addition to the standard operators, we can also use these aforementioned keywords. See our documentation on [If Statement Expressions](https://cleanslatecms.wvu.edu/how-to/theme-development/conditional-logic-loops/if-statement-expressions) to learn more.


### Examples

Check if a page name is equal to a specific string:

```
{% if page.name == "Special" %}
  <strong>This is a special page!!!</strong>
{% endif %}
```

Add an `else` to the above example to catch when the page name is not "Special":

```
{% if page.name == "Special" %}
  <strong>This is a special page!!!</strong>
{% else %}
  This is not a special page.
{% endif %}
```

Add an `elsif` to the example above:

```
{% if page.name == "Special" %}
  <strong>This is a special page!!!</strong>
{% elsif page.name == "Backpage 1" %}
  You won the lottery!
{% else %}
  This is not a special page.
{% endif %}
```

Combine checks using `or`:

```
{% if page.name == "Special" or page.name == "Backpage 1" %}
  <strong>This is a special page!!!</strong>
{% endif %}
```

Check if a variable contains a string:

```
{% assign bearVar = "Bear" %}
{% if bearVar contains "Bear" %}
  <p>Contains a Bear!</p>
{% endif %}
```

Check if the value of a variable is greater than 3.45:

```
{% assign some_variable = 4.25 %}
{% if some_variable > 3.45 %}
  <p>Rendered if <code>some_variable</code> is greater than 3.45.</p>
{% endif %}
```

Render content between a certain time of day:

```
{% assign now = 'now' | to_time %}
{% assign t1 = '8:00 AM' | to_time %}
{% assign t2 = '5:00 PM' | to_time %}
{% if now > t1 and now < t2 %}
  <strong>Displayed between 8 AM and 5 PM daily.</strong>
{% else %}
```

Check against multiple cases using `case/when`:

```
{% assign animal = "Bear" %}
{% case animal %}
  {% when "Wolf" %}
     This is a wolf.
  {% when "Bear" %}
     This is a Bear!
  {% else %}
     This is not a Wolf nor a Bear.
{% endcase %}
```
