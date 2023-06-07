# Github Pages and Jekyll

Jekyll is a static site generator with built-in support for GitHub Pages.

Jekyll is a static site generator with built-in support for GitHub Pages and a simplified build process. Jekyll takes Markdown and HTML files and creates a complete static website based on your choice of layouts. Jekyll supports Markdown and Liquid, a templating language that loads dynamic content on your site.

Jekyll is not officially supported for Windows.

We recommend using Jekyll with GitHub Pages. If you prefer, you can use other static site generators or customize your own build process locally or on another server.

## Configuring Jekyll in your GitHub Pages site

You can configure most Jekyll settings, such as your site's theme and plugins, by editing your \_config.yml file.

Some configuration settings cannot be changed for GitHub Pages sites.

```
lsi: false
safe: true
source: [your repo's top level directory]
incremental: false
highlighter: rouge
gist:
  noscript: false
kramdown:
  math_engine: mathjax
  syntax_highlighter: rouge
```

By default, Jekyll doesn't build files or folders that:

- are located in a folder called /node_modules or /vendor
- start with \_, ., or #
- end with ~
- are excluded by the exclude setting in your configuration file

If you want Jekyll to process any of these files, you can use the include setting in your configuration file.

## Front matter

To set variables and metadata, such as a title and layout, for a page or post on your site, you can add YAML front matter to the top of any Markdown or HTML file.

[Front Matter](https://jekyllrb.com/docs/front-matter/)

## Themes

You can add a Jekyll theme to your GitHub Pages site to customize the look and feel of your site.

You can add a supported theme to your site on GitHub.

To use any other open source Jekyll theme hosted on GitHub, you can add the theme manually.

You can override any of your theme's defaults by editing the theme's files.

## Plugins

You can download or create Jekyll plugins to extend the functionality of Jekyll for your site. For example, the jemoji plugin lets you use GitHub-flavored emoji in any page on your site the same way you would on GitHub. For more information, see "Plugins" in the Jekyll documentation.

GitHub Pages uses plugins that are enabled by default and cannot be disabled:
