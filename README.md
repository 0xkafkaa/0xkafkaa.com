# 0xkafkaa site revamp

The new version of [0xkafkaa.com](https://0xkafkaa.com), built with Zola.
The site combines a personal homepage and a collection of writings with
Tufte typography, sidenotes, and MathJax for mathematical notation.

## Local development

Install Zola and run from the project root:

```sh
zola serve
```

Open the local address printed by Zola. To generate the production site:

```sh
zola build
```

Generated files go into `public/`, which is excluded from Git.

## Project layout

- `zola.toml`: site URL and build configuration.
- `content/writings/`: Markdown articles and writing section metadata.
- `templates/`: shared layout, homepage, writing index, and article templates.
- `static/`: stylesheets, ET Book fonts, and article images.

Add articles under `content/writings/` with TOML front matter containing a
`title` and `date`. The writing section sorts articles by date and applies
the shared article template.
