#### `get_file`

TODO:

  * Change image to include `data-asset-id` attributes, et all.

Target a certain file by its ID.

### Attribute options

![Hover over the thumbnail preview in Files to get a file's ID](https://cleanslatecms.wvu.edu/files/a9f68f88-a1f1-48b9-a353-943970c7007e/542x290?cb=1530742268)

This filter doesn't have any options, but you must pass it a file's ID.

### Example:

```
{% assign myFile = site | get_file: 1234 %} <!-- 👈 Change to your file's ID -->
<p><a download href="{{ myFile.download_url }}">Download {{ myFile.title }}</a></p>
```

Find out the available drops on the [`r:file`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-file) page.
