# Content <!-- omit in toc -->

The `/content` directory is where all the site's (English) Markdown content lives!

See the [markup reference guide](/contributing/content-markup-reference.md) for more information about supported Markdown features.

See the [contributing docs](/CONTRIBUTING.md) for general information about working with the docs.

- [Frontmatter](#frontmatter)
  - [`versions`](#versions)
  - [`redirect_from`](#redirect_from)
  - [`title`](#title)
  - [`shortTitle`](#shorttitle)
  - [`intro`](#intro)
  - [`permissions`](#permissions)
  - [`product`](#product)
  - [`layout`](#layout)
  - [`mapTopic`](#maptopic)
  - [`featuredLinks`](#featuredlinks)
  - [`showMiniToc`](#showminitoc)
  - [`miniTocMaxHeadingLevel`](#minitocmaxheadinglevel)
  - [`allowTitleToDifferFromFilename`](#allowtitletodifferfromfilename)
  - [Escaping single quotes](#escaping-single-quotes)
- [Autogenerated mini TOCs](#autogenerated-mini-tocs)
- [Versioning](#versioning)
- [Filenames](#filenames)
- [Whitespace control](#whitespace-control)
- [Links and image paths](#links-and-image-paths)
  - [Preventing transformations](#preventing-transformations)

## Frontmatter

[YAML Frontmatter](https://jekyllrb.com/docs/front-matter/) is an authoring
convention popularized by Jekyll that provides a way to add metadata to pages.
It is a block of key-value content that lives at the top of every Markdown file.

The following frontmatter values have special meanings and requirements for this site.
There's also a schema that's used by the test suite to validate every page's frontmatter.
See [`lib/frontmatter.js`](../lib/frontmatter.js).

### `versions`

- Purpose: Indicates the [versions](../lib/all-versions.js) to which a page applies.
See [Versioning](#versioning) for more info.
- Type: `Object`. Allowable keys map to product names and can be found in the `versions` object in [`lib/frontmatter.js`](../lib/frontmatter.js).
- This frontmatter value is currently **required** for all pages.
- The `*` is used to denote all releases for the version.

Example that applies to GitHub.com and recent versions of GitHub Enterprise Server:

```yml
title: About your personal dashboard
versions:
  free-pro-team: '*'
  enterprise-server: '>=2.20'
```

Example that applies to all supported versions of GitHub Enterprise Server:
(but not GitHub.com):

```yml
title: Downloading your license
versions:
  enterprise-server: '*'
```

### `redirect_from`

- Purpose: List URLs that should redirect to this page.
- Type: `Array`
- Optional

Example:

```yml
title: Getting started with GitHub Desktop
redirect_from:
  - /articles/first-launch/
  - /articles/error-github-enterprise-version-is-too-old/
  - /articles/getting-started-with-github-for-windows/
```

See [`contributing/redirects`](contributing/redirects.md) for more info.

### `title`

- Purpose: Set a human-friendly title for use in the rendered page's `<title>` tag and an `h1` element at the top of the page.
- Type: `String`
- Optional. If omitted, the page `<title>` will still be set, albeit with a generic value like `GitHub.com` or `GitHub Enterprise`.

### `shortTitle`

- Purpose: An abbreviated variant of the page title for use in breadcrumbs.
- Type: `String`
- Optional. If omitted, `title` will be used.

Example:

```yml
title: Contributing to projects with GitHub Desktop
shortTitle: Contributing to projects
```

### `intro`

- Purpose: Sets the intro for the page. This string will render after the `title`.
- Type: `String`
- Optional.

### `permissions`

- Purpose: Sets the permission statement for the article. This string will render after the `intro`.
- Type: `String`
- Optional.

### `product`

- Purpose: Sets the product callout for the article. This string will render after the `intro` and `permissions` statement.
- Type: `String`
- Optional.

### `layout`

- Purpose: Wrap the page in a custom HTML layout.
- Type: `String` that matches the name of the layout file, without an extension.
For a layout named `layouts/article.html`, the value would be `article`.
- Optional. If omitted, `layouts/default.html` is used.

### `mapTopic`

- Purpose: Indicates whether a page is a map topic. See [Map Topic Pages](#map-topic-pages) for more info.
- Type: `Boolean`. Default is `false`.
- Optional.

### `featuredLinks`

- Purpose: Renders the linked articles' titles and intros on product landing pages and the homepage.
- Type: `Object`.
- Optional.

Example:

```yaml
featuredLinks:
  gettingStarted:
    - /path/to/page
  guides:
    - /guides/example
```

### `showMiniToc`

- Purpose: Indicates whether an article should show a mini TOC above the rest of the content. See [Autogenerated mini TOCs](#autogenerated-mini-tocs) for more info.
- Type: `Boolean`. Default is `true` on articles, and `false` on map topics and `index.md` pages.
- Optional.

### `miniTocMaxHeadingLevel`

- Purpose: Indicates the maximum heading level to include in an article's mini TOC. See [Autogenerated mini TOCs](#autogenerated-mini-tocs) for more info.
- Type: `Number`. Default is `3`. Minimum is `2`. Maximum is `4`.
- Optional.

### `allowTitleToDifferFromFilename`

- Purpose: Indicates whether a page is allowed to have a title that differs from its filename. For example, `content/rest/reference/orgs.md` has a title of `Organizations` instead of `Orgs`. Pages with this frontmatter set to `true` will not be flagged in tests or updated by `script/reconcile-ids-with-filenames.js`.
- Type: `Boolean`. Default is `false`.
- Optional.

### Escaping single quotes

If you see two single quotes in a row (`''`) in YML frontmatter where you might expect to see one (`'`), this is the YML-preferred way to escape a single quote. From [the YAML spec](https://yaml.org/spec/history/2001-12-10.html):

> In single quoted leaves, a single quote character needs to be escaped. This is done by repeating the character.

As an alternative, you can change the single quotes surrounding the frontmatter field to double quotes and leave interior single quotes unescaped.

## Autogenerated mini TOCs

Every article on the help site displays an autogenerated "In this article" section (aka mini TOC) at the top of the page that includes links to all `H2`s and `H3`s in the article by default.

* To make the mini TOC include additional (or fewer) heading levels, you can add [`miniTocMaxHeadingLevel` frontmatter](#miniTocMaxHeadingLevel) to specify the maximum heading level. For example: `miniTocMaxHeadingLevel: 4`
* To disable the mini TOC for a specific article, you can add this frontmatter: [`showMiniToc: false`](#showMiniToc)

Mini TOCs do not appear on product landing pages, category landing pages, or map topic pages.

Make sure not to add hardcoded "In this article" sections in the Markdown source or else the page will display duplicate mini TOCs.

## Versioning

A content file can have **two** types of versioning:

* [`versions`](#versions) frontmatter (**required**)
    * Determines in which the versions the page is available. See [contributing/permalinks](../contributing/permalinks.md) for more info.
* Liquid statements in content (**optional**)
    * Conditionally render content depending on the current version being viewed. See [contributing/liquid-helpers](../contributing/liquid-helpers.md) for more info. Note Liquid conditionals can also appear in `data` and `include` files.

## Filenames

When adding a new article, make sure the filename is a [kebab-cased](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles) version of the title you use in the article's [`title`](#title) frontmatter. This can get tricky when a title has punctuation (such as "GitHub's Billing Plans"). A test will flag any discrepancies between title and filename. To override this requirement for a given article, you can add [`allowTitleToDifferFromFilename`](#allowtitletodifferfromfilename) frontmatter.

## Whitespace control

When using Liquid conditionals in lists or tables, you can use [whitespace control](https://shopify.github.io/liquid/basics/whitespace/) characters to prevent the addition of newlines that would break the list or table rendering.

Just add a hyphen on either the left, right, or both sides to indicate that there should be no newline on that side. For example, this statement removes a newline on the left side:

```
{%- if page.version == 'dotcom' %}
```

These characters are especially important in [index pages](#index-pages) comprised of list items.

## Links and image paths

Local links must start with a product ID (like `/actions` or `/admin`), and image paths must start with `/assets`. These links undergo some transformations on the server side to match the current page's language and version. The handling for these transformations lives in [`lib/rewrite-local-links`](lib/rewrite-local-links.js) and [`lib/rewrite-asset-paths-to-s3`](lib/rewrite-asset-paths-to-s3.js).

For example, if you include the following link in a content file:

```
/github/writing-on-github/creating-a-saved-reply
```
When viewed on GitHub.com docs, the link gets rendered with the language code and version:
```
/en/free-pro-team@latest/github/writing-on-github/creating-a-saved-reply
```
and when viewed on GitHub Enterprise Server docs, the version is included as well:
```
/en/enterprise-server@2.20/github/writing-on-github/creating-a-saved-reply
```

The transformation is a little different for image paths. If you include the following image path in a content file:

```
/assets/images/help/profile/follow-user-button.png
```
when viewed on GitHub Enterprise Server docs, the path gets rewritten to include S3:

```
https://github-images.s3.amazonaws.com/enterprise/2.20/assets/images/help/profile/follow-user-button.png
```

### Preventing transformations

Sometimes you want to link to a Dotcom-only article in Enterprise content and you don't want the link to be Enterprise-ified. To prevent the transformation, write the link using HTML and add a class of `dotcom-only`. For example:

```
<a href="/github/site-policy/github-terms-of-service" class="dotcom-only">GitHub's Terms of Service</a>
```

Sometimes the canonical home of content moves outside the docs site. None of the links included in [`lib/redirects/external-sites.json`](/lib/redirects/external-sites.json) get rewritten. See  [`contributing/redirects.md`](/contributing/redirects.md) for more info about this type of redirect.