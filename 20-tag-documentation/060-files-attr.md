#### `{% files.{attr} %}`

A tag used to loop through files like images, PDF's, audio files and more.

### Files Filters

The `files` tag uses a parent `filter_files` filter that takes the following arguments:

`tags` - A comma separated list of labels/tags to filter by. Do not include spaces. Eg: `hello,my-special-label,News_Events`.

`types` - Specify what types of files you would like to return. Eg: `image,audio,document,file,pdf,video`.

`tags_match` - Specify `any`, `all` or `none` as to how to match which of the referenced labels. `any` means any file with any one of the labels. `all` means the file must have every label specified in the list. `none` means files that _don't_ have the specified labels.

`order` - The order you want to display the files. Valid values are: `name`, `title`, `alt_text`, `description`, `size` and `uploaded_at`.

`title` - Specify the title of a file or files you want to filter by.

`reverse` - Reverse the order of the output. Value: boolean.

`random` - Randomize the output of the files loop. Value: boolean.

`offset` - Used for pagination of files. Used in conjunction with `limit` and page parameters. Default: 1. Eg: `offset: 2` or `offset: params.page`.

`limit`  - Limit the number of files output by the loop. Value: integer. Default: 50.

### Examples

Output linked images based off of a label via a page slug:

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

Output a list of files with links. If the file is an image, output the image to an image tag along with the image path and URL:

```
{% assign files = site.files | filter_files: tags: "download,wvu,profile", types: "", tags_match: "any", order: "uploaded_at", limit: 5, offset: params.page %}
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
