---
name: site-and-pages
description: Design a website hosted on tinycms, or change how it looks and is laid out. Use when the person asks for a new design or a redesign, or about the site's look, colours, fonts, logo, header, footer, navigation menu, home page, templates and starters, page blocks, media uploads, custom CSS, or setting up a new site.
---

# Site look, pages and media

tinycms hosts the site and serves whatever design you give it, so the design is yours to make. You are not limited to the templates: start from one or from nothing, set the colours, type and layout, build each page from blocks, and write custom CSS for the rest. Ask what the site should feel like, or propose a direction and show it in a preview.

The site's look, header, footer and home page are settings on one site document, not pages. `get_site` reads the working copy; `update_site` changes it. Changes stay unpublished until the person says yes to publishing the site document (see the `working-with-tinycms` skill).

## Look

- Read `guide_read` with name `site` once per chat: it lists every setting and its allowed values.
- `preset` (classic, editorial, minimal) is the base. `colors` (background, text, accent, muted, button as hex), `fonts` (heading and body: a preset or any Google Fonts family by name, served from the site itself) and `layout` (home, width, spacing, corners, header shape, logo size, menu style, image shape, photo treatment, heading scale) override it.
- Pass only the fields you are changing. A list, such as `navigation.header`, replaces the whole list, so read it first and send it back whole.
- Custom CSS goes in `customCss`, written against the stable hooks in `guide_read` with name `css` only. Never target utility classes or markup nesting. Prefer tokens for colours, fonts and layout, and CSS for the rest.
- Scripts and head or body HTML are not available over MCP. If the person needs them, say that an account admin adds them in the app under Website › Manage › Code & tracking.

## Header, footer and navigation

- `navigation.header`: up to 6 entries, each `{ label, href }` or a dropdown `{ label, children: [...] }`. `navigation.cta` is one button at the end of the header. `navigation.phone` shows a number before it.
- `navigation.footer` (one row, up to 12 links), `navigation.footerColumns` (up to 4 columns), `navigation.footerText` (copyright or address) and `navigation.social` (network and href).
- `href` is a site path such as `/pricing` or `/articles`, or a full URL.
- `business` holds who runs the site (type, name, phone, email, address) for search results.

## Home page

- By default the home page lists published articles. Set `layout.homePage` to a page's slug to show that page at `/` instead; the article list then lives at `/articles`.
- `layout.home` picks feed, list or grid for the article list.

## Pages and blocks

- A page is a list of blocks. `guide_read` with name `blocks` lists every block and its fields. `get_page`, then `update_page` with the whole list.
- A form shows on a page through a `{ type: "form", formId }` block.
- `run_preflight` checks a page, and `get_preview_url` with `pageId` opens the preview on it.
- Pages that link to each other go live together with `publish_pages` under one yes.

## Templates and starters

- `guide_read` with name `starters` lists the templates: each is a look and a shape (the pages a site of that kind has, their blocks, header, footer, a contact form and the home page).
- `apply_starter` with a `starterId` creates those pages as working copies. Nothing is published. The sample copy becomes neutral placeholder text, marked so you can find it. Offer to rewrite the placeholder blocks in the person's words and to set `business` when they give an address.
- `apply_starter` with `only: "look"` switches an existing site to a template's look and keeps every page, form and article.

## Media

- Files the person attached in this chat: `import_chat_files` adds them to the media library by reference and returns each file's URL. If it fails for a file, or your client passes no file references, use `request_media_upload`.
- Photos and files from the person's phone or computer: `request_media_upload` returns a link where they upload. Send it with the note it returns. When they are done, call it again with the `requestId` for the URLs.
- A file at a public URL: `import_media_from_url`. Images return a URL for an article hero, an image block or a social post. Video is ready in minutes; `list_media` then gives its asset id.
- `upload_media` spends the person's tokens. Use it only for a chart or diagram you drew as SVG, or a small icon. Never for photos.
- `attach_media` records an image in a named slot (such as an article's lead image or the site's logo). Give every image an `alt` description.
- The site's logo, cover and tab icon are `imagery` on the site document. The tab icon is a square PNG of at least 180×180 pixels.
