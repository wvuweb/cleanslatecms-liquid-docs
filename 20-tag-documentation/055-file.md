#### `file.{attr}`

TODO:

  * Is 👇 correct?
  * Consider adding `svg` to the `CONTENT_READABLE_FILE_EXT`:
    * https://github.com/wvuweb/cleanslate/blob/dev/app/lib/slate/liquid/drops/file_drop.rb#L6
  * FIX: `background_styler`
  * CHECK: `first_random_image_tagged_with` and `get_file` (totally guessed on these! Probably incorrect)

This tag references individual files and will always be used inside a [`files.{attr}`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-files-attr) loop.

### Attribute options

`download_url` - Get the URL to download the file.

`id` - Get the file's unique ID.

`title` - Get the file's title as is listed in the file's properties in CleanSlate.

`filename` - Get the filename as is lsited in the file's properties in CleanSlate.

`uploaded_at` - Get the time the file was uploaded. You can pass this through the date filter (eg `| date: "%Y-%m-%d"`) to change the output of the date string.

`is_image` - Checks if the file is an image format.

`image_dimensions` - Returns the original image dimensions of a file in a NxM format (eg: `100x150`).

`content` - Outputs the contents of a file if it uses one of the following formats: `xml`, `json`, `html`, `css`, `js`, `txt`, `text`, `csv`.

### File filters

`date` - Format a valid timestring into the format you want. See documentation for [`date`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-date-format).

`image_url` - Output an image's fully qualified URL in a loop. You can optionally pass it a specific size to output. Eg: `{{ file | image_url }}` OR `{{ file | image_url: size: "250x" }}`.

`image_path` - Get the relative path to an image. Eg: `{{ file | image_path }}`.

`background_styler` - Output a background image...

`first_random_image_tagged_with` - Get the first random image tagged with a specific label. Eg: `{{ file | first_random_image_tagged_with: tag: "hero-background" }}`

`get_file` - Get a specific file by targeting it's ID. Eg: `{{ file | get_file: id: "1234" }}`

### Examples

Loop through files labelled with `download`, `wvu`, or `profile` and return their properties:

```
{% assign files = site.files | filter_files: tags: "download,wvu,profile", types: "", tags_match: "any", order: "uploaded_at" %}
<ul class="files">
  {% for file in files.all %}
    <li class="span4">
      <span>{{ forloop.index }} - </span>
      <a href="{{ file.download_url }}" data-asset-id="{{ file.id }}">{{ file.title }}</a>
      <small>({{ file.filename }} uploaded {{ file.uploaded_at | date: "%Y-%m-%d" }})</small>
      <p>
        {% if file.is_image %}
          <img src="{{ file | image_url: size: "250x" }}" /> <br/>
          Original Image Dimensions: {{ file.image_dimensions }} <br/>
          Image Path: {{ file | image_path }} <br/>
          Image URL: {{ file | image_url }}
        {% endif %}
      </p>
    </li>
  {% endfor %}
</ul>
```
