#### `page.previous_sibling` and `page.next_sibling`

In CleanSlate, it is possible to access the previous and next pages relevant to the current page, based on page ordering, with the  `page.previous_sibling` and `page.next_sibling` tags.

For example, you could create a pager to navigate through a set of sibling pages as follows:

```
<ul class="pager">
  <li class="previous"><a href="{{ page.previous_sibling.url }}">&larr; {{ page.previous_sibling.name }}</a></li>
  <li class="next"><a href="{{ page.next_sibling.url }}">{{ page.next_sibling.name }} &rarr;</a></li>
</ul>
```
