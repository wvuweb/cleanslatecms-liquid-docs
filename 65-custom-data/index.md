# Custom Data

Custom page data in Liquid behaves almost identically to how it does in Radius—with one key difference: how you call the custom data in your template:

Radius: `<r:page:data name="key_1"/>`

Liquid: `{{ page.data.key_1 }}`

## Custom site data

Again, custom site data in Liquid behaves almost identically to how it does in Radius—it just has a slightly different syntax when included in templates:

Radius: `<r:site:data name="site_1" />`

Liquid: `{{ site.data.site_1 }}`
