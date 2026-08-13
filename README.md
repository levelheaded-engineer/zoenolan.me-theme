# zoenolan.me theme - Hugo theme
A minimal and clean theme for Hugo with a markdown-ish UI, used by
[zoenolan.me](https://www.zoenolan.me).

Forked from [Archie](https://github.com/athul/archie), which is itself forked from
[Ezhil](https://github.com/vividvilla/ezhil). See
[Differences from Archie](#differences-from-archie) for what has changed since the fork; everything
else below is inherited and still applies.

![](/images/theme.png)
![](/images/archie-dark.png)
## Feature
- Google Analytics Script
- Callouts
- Tags
- Search
- Auto Dark Mode(based on system theme)
- Dark/Light Mode toggle
- tl:dr; frontamatter
- Table of contents
- Cache busting for CSS files
- Disqus Comments
- Three-column footer with social icons, Roman-numeral copyright year and a colophon link
- Letterbird contact-form shortcode
- `elsewhere` section layouts with RSS

## Installation
In your Hugo website directory, create a new folder named themes and clone the repo
```bash
$ mkdir themes
$ cd themes
$ git clone https://github.com/levelheaded-engineer/zoenolan.me-theme.git
```
Edit the `hugo.toml` file with `theme="zoenolan.me-theme"`
For more information read the official [setup guide](https://gohugo.io/installation/) of Hugo.

If you encounter any issues with Google Analytics, update Hugo to v0.125.0 or
later and make sure your using the latest version of the theme.

## Writing Posts
Create a new `.md` file in the *content/posts* folder
```yml
---
title: Title of the post
description:
date:
tldr: (optional)
draft: true/false (optional)
tags: [tag names] (optional)
toc: true/false (optional)
---
```

## Credits
Forked from [Archie](https://github.com/athul/archie) by Athul Cyriac Ajay, which was forked from
[Ezhil Theme](https://github.com/vividvilla/ezhil). Licensed under MIT License.
Inspired by design of blog.jse.li

----

## Differences from Archie

### Footer

The footer is a three-column layout: copyright on the left, social icons in the middle, colophon link
on the right.

The copyright year is rendered in Roman numerals, in `© YEAR name` order, taking the name from the
site's `copyright` config value.

The right column links to a colophon page if one exists. Create `content/colophon/index.md` and the
link appears automatically, using that page's title; with no such page the column stays empty.

```yaml
---
title: "Colophon"
hideDate: true
---
```

### Letterbird shortcode

Embeds a [Letterbird](https://letterbird.co) contact form. The username falls back to
`params.letterbirdUsername`, so pages can usually call the shortcode bare.

```toml
[params]
  letterbirdUsername = "yourusername"
```

```markdown
{{< letterbird >}}
{{< letterbird username="someoneelse" subject="Hello" showheader="true" >}}
```

### `hideDate` front matter

Suppresses the "Posted on" line on a single page — useful for pages like Contact or CV that are not
dated posts.

```yaml
---
title: "Contact"
hideDate: true
---
```

### `elsewhere` section

Layouts for an `elsewhere` section that lists dated, tagged entries with their content inline rather
than linking out to full pages, plus a matching RSS output. Entries support `extra_link` and
`extra_link_text` front matter for an additional link in the entry heading.

### Other changes

- The home page renders its own content directly instead of a paginated post list.
- The paginator shows an "X of Y" page count between the prev/next links.
- Heading hash marks (`#`, `##`) are no longer prepended to headings.

----

## Config Options

### Custom CSS
Custom CSS files can be included though the `customcss` config parameter.

Note: CSS files should be placed under the `assets` directory e.g. `assets/css/first.css`.

```toml
[params]
	customcss = ["css/first.css", "css/second.css"]
```

### Callouts

There are five different types of callout, including this themes original callout and a custom one as well. These callouts are compatible with both light and dark theme modes. 

![Screenshot from 2025-01-04 19-22-43](https://github.com/user-attachments/assets/bcaf7c3c-2339-449f-8bcb-8a2906d7ddcf)


#### Original

This steup is to ensure backwards compatibility for previous callouts.

```markdown                                                                                                                                                                                                    
{{< callout emoji="⚡️" text="Original callout." >}}
```

#### Alert
```markdown
{{< callout type="alert" text="This is an alert callout." >}}
```

#### Custom

This include the ability to set your own callout emoji, title, and css style element.

```markdown
{{< callout type="custom" emoji="⚡️" title="Custom callout" text="This is custom text for a custom callout." style="background-color: transparent; border: 3px solid #d340e0;" >}}
```

#### Tip

```markdown
{{< callout type="tip" text="This is a tip callout." >}}
```

#### Warning

```markdown
{{< callout type="warning" text="This is a warning callout." >}}
```

### Search

Archie ships with an opt-in search page backed by a Hugo-generated JSON index.

1. Create a search page:

```yaml
---
title: "Search"
layout: "search"
outputs:
  - html
  - json
---
```

2. Add the page to your main menu if you want it linked in the header:

```toml
[[menu.main]]
name = "Search"
url = "/search/"
weight = 5
```

The generated search page indexes the same content surface as the home page when
`params.mainSections` is set. Otherwise it falls back to all regular pages,
excluding hidden content and the search page itself.

## Example Config

```toml
baseURL = "https://www.example.com"
languageCode = "en-us"
title = "Your Site"
theme="zoenolan.me-theme"
copyright = "Your Name" # rendered as "© MMXXVI Your Name" — don't include the © yourself
# Code Highlight
pygmentsstyle = "monokai"
pygmentscodefences = true
pygmentscodefencesguesssyntax = true

disqusShortname = "yourDisqusShortname"

[pagination]
  pagerSize = 3 # articles per page

[params]
	mode="auto" # color-mode → light,dark,toggle or auto
	useCDN=false # don't use CDNs for fonts and icons, instead serve them locally.
	subtitle = "Minimal and Clean [blog theme for Hugo](https://github.com/levelheaded-engineer/zoenolan.me-theme)"
	letterbirdUsername = "yourusername" # default user for the letterbird shortcode
	mathjax = true # enable MathJax support
	katex = true # enable KaTeX support

# Social Tags

[[params.social]]
name = "GitHub"
icon = "github"
url = "https://github.com/athul/archie"

[[params.social]]
name = "Twitter"
icon = "twitter"
url = "https://twitter.com/athulcajay/"

[[params.social]]
name = "GitLab"
icon = "gitlab"
url = "https://gitlab.com/athul/"

# Main menu Items

[[menu.main]]
name = "Home"
url = "/"
weight = 1

[[menu.main]]
name = "All posts"
url = "/posts"
weight = 2

[[menu.main]]
name = "About"
url = "/about"
weight = 3

[[menu.main]]
name = "Tags"
url = "/tags"
weight = 4
```
---

Archie, the theme this one is forked from, is the work of Athul Cyriac Ajay — if you like it please
consider supporting them on [BuymeACoffee](https://www.buymeacoffee.com/athulca)

<a href="https://www.buymeacoffee.com/athulca" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-red.png" alt="Buy Me A Coffee" height="41" width="174" ></a>
