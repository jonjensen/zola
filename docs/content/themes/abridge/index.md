
+++
title = "abridge"
description = "A fast and lightweight Zola theme using semantic html, abridge.css class-light CSS, and No JS."
template = "theme.html"
date = 2022-05-16T01:14:18-07:00

[extra]
created = 2022-05-16T01:14:18-07:00
updated = 2022-05-16T01:14:18-07:00
repository = "https://github.com/Jieiku/abridge.git"
homepage = "https://github.com/jieiku/abridge"
minimum_version = "0.14.1"
license = "MIT"
demo = "https://jieiku.github.io/abridge-demo/"

[extra.author]
name = "Jake G (jieiku)"
homepage = "https://github.com/jieiku"
+++        

# Abridge Zola Theme

Abridge is a fast and lightweight Zola theme using semantic html, class-light [abridge.css](https://github.com/jieiku/abridge.css), and No JS.

![abridge](screenshot.png)

## Demo

[https://jieiku.github.io/abridge-demo/](https://jieiku.github.io/abridge-demo/)

## Requirements

This theme requires version 0.14.1 or later of [Zola](https://www.getzola.org/documentation/getting-started/installation/)

## Quick Start

```bash
git clone https://github.com/jieiku/abridge
cd abridge
zola serve
# open http://127.0.0.1:1111/ in the browser
```

## Installation
The Quick Start example shows you how to run the theme directly as a site.
Next we will use abridge as a theme to a NEW site.

### Step 1: Create a new zola site

```bash
zola init mysite
```

### Step 2: Install abridge

Download this theme to your themes directory:

```bash
cd mysite/themes
git clone https://github.com/jieiku/abridge.git
```

Or install as a submodule:

```bash
cd mysite
git init  # if your project is a git repository already, ignore this command
git submodule add https://github.com/jieiku/abridge.git themes/abridge
```

### Step 3: Configuration

Enable the theme in your `config.toml` in the site directory:

```toml
theme = "abridge"
```

Or copy the `config.toml` from the theme directory to your project's
root directory, and uncomment the theme line:

```bash
cp themes/abridge/config.toml config.toml
sed -i 's/^#theme = "abridge"/theme = "abridge"/' config.toml
```

### Step 4: Add new content

You can copy the content from the theme directory to your project:

```bash
cp -r themes/abridge/content .
```

You can modify or add new posts in the content directory as needed.

### Step 5: Run the project

Just run `zola serve` in the root path of the project:

```bash
zola serve
```

Zola will start the development web server making your site accessible by default at
`http://127.0.0.1:1111`. Saved changes will live reload in the browser.

## Customization

You can customize your configurations, templates and content for yourself. Look
at the `config.toml`, `content` files, and templates files in this
repo for an idea.

### Number of Items per page for pagination

To change the number of items per page edit: `abridge/content/_index.md` and change the value for `paginate_by`

### Page width

You can set the overal page width by editing `themes\abridge\sass\_variables.scss` file, and adjusting these two lines:

```scss
$mw:50% !default;// max-width
$mb:1200px !default;// value at which to switch from fluid layout to using max-width
```

### Colors and Styles

Colors and style are handled by the sass files of [abridge.css](https://github.com/jieiku/abridge.css)

To change colors of this theme all you need to do is edit `/themes/abridge/sass/themes/_auto.scss`
then in the root of your site type `zola build` which will regenerate your site, this is similar to what zola serve does, except it does not facilitate serving the site.
This is also the way you should generate your site to serve it by a real webserver such as nginx.

### Global Configuration

There are some configuration options that you can customize in `config.toml`.

#### Configuration options before `extra` options

Set the authors's taxonomies for the site.

```toml
taxonomies = [
  {name = "authors"},
]
```

Use search function for the content.

```toml
build_search_index = true
```

​The search is the only thing that requires javascript in this this theme.

If you set `build_search_index` to false then the javascript file will no longer be loaded.

The default elasticlunr search is currently used, I may eventually switch this out for something else.

#### Configuration options under the `extra`

The following options should be under the `[extra]` in `config.toml`

- `recent = true` - This enabled the Recent posts box visible on the top right.
- `recent_items = 9` - The number of items to display in the recent posts box
- `footer_credit = true` - This enables the powered by zola and abridge line in the footer.
- `textlogo` - The Text based logo in the top left corner
- `sitedesc` - This add the site description just below the text based logo.
- `author` - Used for articles to denote the author.
- `keywords` - This is used for SEO, I am however still working on the SEO related fields, they are likely not 100% correct yet.
- `banner` - Image to use in seo related cards, this will be the fallback image if the individual articles does not provide one, still a work in progress.
- `menu` - This is an array of links to display at the top right corner of the page
- `menu_footer` - This is an array of links to display in the footer of the page
- `extra.social` - These are the options for the social icons in the footer, and a couple are also used in SEO related meta tags, still a work in progress.

Additionally you should configure which social icons you plan to use. (makes the css file size smaller)

open `themes/abridge/sass/_variables.scss`

To simply turn them all off you can set `$enable-icons: false`
Otherwise to turn on only the ones you need you would set `$enable-icons: true`
Then enable only the icons you need, eg for mail you would set `$icon-mail: true`
You should then disable all the icons that you do not use, as this will decrease the final size of your css file.
The difference in size is NOT a lot, without icons its ~4kb, with all the social icons its ~12kb.
There are also some general purpose icons you can use, they are disabled by default.

The theme requires tags and categories taxonomies to be enabled in your `config.toml`:

```toml
taxonomies = [
    # You can enable/disable RSS
    {name = "categories", rss = true},
    {name = "tags", rss = true},
]
```

### Top and Footer menus
Set a field in `extra` with a key of `menu` and `menu_footer`.
If a link should have a trailing slash at the end of the url set `slash = true`.

```toml
# This is the default menu
menu = [
    {url = "/", name = "Home", slash = true},
    {url = "/about/", name = "About", slash = true},
    {url = "/posts/", name = "Posts", slash = true},
    {url = "/categories/", name = "Categories", slash = true},
    {url = "/tags/", name = "Tags", slash = true},
]
menu_footer = [
    {url = "/", name = "Home", slash = true},
    {url = "/about/", name = "About", slash = true},
    {url = "/contact/", name = "Contact", slash = true},
    {url = "/privacy/", name = "Privacy", slash = true},
    {url = "/sitemap.xml", name = "Sitemap", slash = false},
]
```

### SEO and Header Tags

Some SEO Tags have been added as well as some important head tags for browser compatibility.

you can review them in the head section of templates/base.html, all configurable values should be in config.toml under config.extra

SEO is still a work in progress, will be performing more testing and updates as time allows.

### Templates

All pages are extend to the `base.html`, and you can customize them as need.

## Reporting Issues

We use GitHub Issues as the official bug tracker for **abridge**. Please
search [existing issues](https://github.com/jieiku/abridge/issues). It’s
possible someone has already reported the same problem.

If your problem or idea is not addressed yet, [open a new issue](https://github.com/jieiku/abridge/issues/new).

## Contributing

We'd love your help! Especially with fixes to issues.
The overall idea behind abridge is to be lightweight and fast, and to use zero javascript other than the search.

## License

**abridge** is distributed under the terms of the
[MIT license](https://github.com/jieiku/abridge/blob/master/LICENSE).

        