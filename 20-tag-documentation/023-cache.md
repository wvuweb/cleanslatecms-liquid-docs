#### `{% cache %}`

Manually caches content for a given number of minutes that may be expensive to render.

This cache uses a strict time-based expiration. Editing the theme, site settings or page content will not bust the cache. This is particularly useful for large/resource intensive navigation menus that take a long time to build/render. Standard caching for menus is busted anytime changes are made to the theme, site, or any page setting or content.

For a large site that is actively maintained/edited during the day, this could prove costly for performance. Manually caching with this tag for a set time period could help alleviate this performance burden.

**Note:** It's best to use this tag only when necessary as it will cause confusion between the [normal CleanSlate cache](https://cleanslatecms.wvu.edu/how-to/content-publishing/basic-editing/editing-content/cache). In other words, use this reactively instead of proactively.

### Attribute options

`duration` - The number of minutes to cache the content inside this tag for.

`key` - A unique string. Changing this value will invalidate the current cache cycle.

### Example

```
{% cache key: "cache_version_001", duration: 30 %}
  {% site_menu max_depth: 3 %}
{% endcache %}
```
