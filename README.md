# Static Site Generator

A static site generator written from scratch in Python. It converts a folder of Markdown files into a styled HTML website, with no third-party Markdown or templating libraries.

## How it works

```
content/*.md ──► Markdown blocks ──► inline text nodes ──► HTML node tree ──► template.html ──► docs/*.html
static/     ──────────────────────────── copied as-is ─────────────────────────────────────────► docs/
```

1. **Block parsing** (`markdown_blocks.py`): splits a document into blocks and classifies each as a paragraph, heading, code block, quote, unordered list or ordered list.
2. **Inline parsing** (`inline_markdown.py`): splits text into typed nodes for bold, italic, code, links and images, using delimiter splitting and regex extraction.
3. **HTML tree** (`htmlnode.py`, `textnode.py`): an `HTMLNode` / `LeafNode` / `ParentNode` hierarchy that renders itself recursively to HTML.
4. **Page generation** (`gencontent.py`): walks `content/` recursively, pulls the page title from the first `# heading`, injects content into `template.html` and rewrites links for a configurable base path.
5. **Static assets** (`copystatic.py`): recursively copies `static/` (CSS, images) into the output folder.

Output goes to `docs/`, so the site can be served directly with GitHub Pages.

## Usage

```bash
./main.sh    # build locally with base path "/"
./build.sh   # build for GitHub Pages under /REPO_NAME/
./test.sh    # run the unit tests
```

## Tests

44 unit tests (Python `unittest`) cover text nodes, HTML rendering, inline Markdown splitting, link/image extraction, block classification and title extraction.

## Tech stack

Python 3 (standard library only) · HTML / CSS
