#### `{% theme_image_url %}`

Gets the relative path to an image in your theme's `images` directory. It will include the current ten digit cache string (eg: `1234567890`).

**NOTE:** All images used with this tag must reside in a directory called `images` (not `img` or any other variant of the word).

### Attributes

`name` - The file name of the image in your theme's `images` directory.

### Example

Linking an image tag in HTML in a template:

```
<img src="{% theme_image_url name: "my_file_name.jpg" %}" alt="My alt text">
<!-- Output: <img src="/images/1611349829/my_file_name.jpg" alt="My alt text"> -->
```

If your image doesn't exist at the root of the `images` directory, include the path:

```
<img src="{% theme_image_url name: "path/to/my-jpgs/my_file_name.jpg" %}" alt="My alt text">
<!-- Output: <img src="/images/1611349829/path/to/my-jpgs/my_file_name.jpg" alt="My alt text"> -->
```

If, for some reason, you wanted to print out the path, you could use `theme_image_url` alone:

```
<p><strong>The path:</strong> {% theme_image_url name: "my_file_name.jpg" %}</p>
<!-- Output: The path: /images/1611349829/my_file_name.jpg -->
```
