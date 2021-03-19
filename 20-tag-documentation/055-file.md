#### `file.{attr}`

TODO:

  * Is 👇 correct?
  * Consider adding `svg` to the `CONTENT_READABLE_FILE_EXT`:
    * https://github.com/wvuweb/cleanslate/blob/dev/app/lib/slate/liquid/drops/file_drop.rb#L6
  * Consider making both `label` AND `tag` work with `first_random_image_tagged_with`:
    * https://github.com/wvuweb/cleanslate/blob/dev/app/lib/slate/liquid/filters/file_filters.rb#L31

This tag references individual files and will always be used inside a [`files.{attr}`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-files-attr) loop.

### Attribute options

`download_url` - Get the URL to download the file.

`id` - Get's the unique ID of the file. Returns a number (eg: `1234`). Hover over the file's preview thumbnail in Files to find the file's ID.

`title` - Get the file's title as is listed in the file's properties in CleanSlate.

`name` - Get the file's name as is listed in the file's properties in CleanSlate.

`alt_text` - Get the file's alt text as is listed in the file's properties in CleanSlate.

`filename` - Get the filename as is lsited in the file's properties in CleanSlate.

`description` - Get the images's description as is listed in the images's properties in CleanSlate.

`uploaded_at` - Get the time the file was uploaded. Returns a valid timestamp (eg: `2021-02-23 16:37:27 -0500`). You can pass this through the date filter (eg `| date: "%Y-%m-%d"`) to change the output of the date string.

`created_at` - Get the time a file was created. Returns a valid timestamp (eg: `2021-02-23 16:37:27 -0500`).

`is_image` - Checks if the file is an image format.

`image_dimensions` - Returns the original image dimensions of a file in a NxM format (eg: `100x150`).

`content` - Outputs the contents of a file if it uses one of the following formats: `xml`, `json`, `html`, `css`, `js`, `txt`, `text`, `csv`.

### File filters

`date` - Format a valid timestring into the format you want. See documentation for [`date`](https://cleanslatecms.wvu.edu/how-to/theme-development/tag-index/r-date-format).

`image_url` - Output an image's fully qualified URL in a loop. You can optionally pass it a specific size to output. Eg: `{{ file | image_url }}` OR `{{ file | image_url: size: "250x" }}` or `{{ file | image_url: size: "250x500" }}`.

`image_path` - Get the relative path to an image. Eg: `{{ file | image_path }}`.

`background_styler` - Output a CSS `background-image` as an inline style on an element. See example below. 

`first_random_image_tagged_with` - Get the first random image tagged with a specific label. See example below.

`get_file` - Get a specific file by targeting it's ID. See example below.

### Examples

Get a random image based on a label:

```
{% assign randomImage = site | first_random_image_tagged_with: tag: "backpage-1-thumbnail" %}
{% assign randomImage_url = randomImage | image_url: size: "1200x630" %}
<img src="{{ randomImage_url }}" alt="{{ randomImage.alt_text }}">
```

☝️ Taking that one step further, assign a dynamic label based on the page slug:

```
{% assign page_slug_label = page.slug | append: "-thumbnail" %}
{% assign randomImage = site | first_random_image_tagged_with: tag: page_slug_label %}
{% assign randomImage_url = randomImage | image_url: size: "1200x630" %}
<img src="{{ randomImage_url }}" alt="{{ randomImage.alt_text }}">
```

☝️ See more examples like these on the [Get a random image, file, or blog article](https://cleanslatecms.wvu.edu/how-to/theme-development/random-image-file-or-blog-article) page.

Output markup for a lightbox gallery (extra CSS & JS required):

```
{% capture gallerypage %}{{ page.slug }}-gallery{% endcapture %}
{% assign images = site.files | filter_files: tags: gallerypage, types: "image" %}
{% for image in images.all %}
  <div class="image-container">
    <a href="{{ image | image_url: size: "960x640" }}" title="{{ image.description }}">
      <img src="{{ image | image_url: size: "480x320" }}" alt="{{ image.alt_text }}" />
    </a>
  </div>
{% endfor %}
```

☝️ Label images `PAGE-SLUG-gallery` to have images output via this loop. Change `PAGE-SLUG` to you're page's actual slug (eg: `about-us` becomes `about-us-gallery`).

Background styler example:

```
{% assign bgStyler = "backpage-1-thumbnail" | background_styler %}
<div class="my-div" {{ bgStyler }}>
  <p>The CSS background image is output on the parent <code>div</code>.</p>
</div>

<!-- Returns: -->
<div class="my-div" style="background-image: url(http://example.wvu.edu/files/24271fb1-0561-4e5d-a750-0c0fdb44985d/1780x1780?cb=1614116587)">
  <p>The CSS background image is output on the parent <code>div</code>.</p>
</div>
```

☝️ See more examples like this on the [Get a random image, file, or blog article](https://cleanslatecms.wvu.edu/how-to/theme-development/random-image-file-or-blog-article) page.

Get the first random image tagged with a label:

```
{% assign my_random_image = site | first_random_image_tagged_with: tag: "backpage-1-thumbnail" %}
<img src="{{ my_random_image | image_url: size: "300x" }}" alt="{{ my_random_image.alt_text }}" />
```

Get a file based off of a file ID:

```
{% assign myFile = site | get_file: 1234 %} <!-- 👈 Change to your file's ID -->
<p><a download href="{{ myFile.download_url }}">Download {{ myFile.title }}</a></p>
```

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
