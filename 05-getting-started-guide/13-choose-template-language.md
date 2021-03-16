# Choose a template language

CleanSlate supports two different templating languages: [Radius](https://github.com/jlong/radius) and [Liquid](https://shopify.github.io/liquid/).

Most themes use Radius and don't need to be configured to do so. You can start writing things like `<r:page:name />` and it will just work.

If you want to use Liquid, open your theme's `config.yml` file at the root and paste the following:

```
engine: liquid
```

This tells CleanSlate to use the Liquid templating language with your theme.

## Why use Liquid?

Until 2021, CleanSlate ran 100% on the Radius templating language. As themes became more and more complex, we started to notice Radius templates taking a _long_ time to render. The [cache](https://cleanslatecms.wvu.edu/how-to/content-publishing/basic-editing/editing-content/cache) was the only thing preventing downtime.

In late 2020, WVU implemented the Liquid templating language to work with CleanSlate. We immediately noticed **performance increases of 80-90%** in themes we converted from Radius to Liquid. Page loads that once took 8 seconds were now less than a second.

Starting mid-summer 2021, all new themes should use the Liquid templating language in an effort to maximize performance and to minimize resource drain on the entire system. This is good for your users and good for WVU.
