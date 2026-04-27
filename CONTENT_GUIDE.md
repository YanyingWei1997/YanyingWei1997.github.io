# Content Maintenance Guide

This site uses two static homepage pages instead of a translation plugin:

- English homepage: `_pages/about.md`, served at `/`
- Chinese homepage: `_pages/about.zh.md`, served at `/zh/`

Follow the rules below when adding or updating content.

## Language Rules

- Every page or post that has a language version must set `lang`.
- Use `lang: en` for English content.
- Use `lang: zh` for Chinese content.
- Do not rely on `site.active_lang` or `jekyll-polyglot`; this site does not use Polyglot.
- The top navigation detects language from `page.lang`.

Example:

```yaml
---
layout: post
title: "Post title"
date: 2026-04-28
description: "Short description."
cover_image: "/images/example-cover.png"
permalink: /blog/example-en/
lang: en
---
```

## Homepage Sections

When adding major homepage content, update both language pages deliberately:

- English content goes in `_pages/about.md`.
- Chinese content goes in `_pages/about.zh.md`.
- If the Chinese homepage should mirror the English section, copy the same HTML structure and only translate the visible text when needed.
- Keep anchor IDs stable, because navigation links depend on them.

Current important anchors:

- English: `about-me`, generated heading anchors for `News`, `Publications`, `Education`, `Teaching`, `Funding & Honors`, `Notes`
- Chinese: `about-me`, `news`, `publications`, `education`, `teaching`, `notes`

## Navigation

Navigation data files:

- English navigation: `_data/navigation.yml`
- Chinese navigation: `_data/navigation_zh.yml`

Do not use a data filename with dots such as `navigation.zh.yml`. Older Liquid/Jekyll behavior can make that hard to read reliably.

When adding a new homepage section:

1. Add the content section to the correct homepage page.
2. Add or confirm the section anchor.
3. Update the matching navigation data file.
4. Use root-based URLs, for example `/zh/#notes`, not relative URLs like `notes`.

## Images And Covers

Use root-based image paths everywhere content may render under `/zh/`:

```html
<img src="{{ '/images/example.png' | relative_url }}" alt="Description">
```

or in post front matter:

```yaml
cover_image: "/images/example-cover.png"
```

Avoid paths like `images/example.png` in the Chinese homepage. Under `/zh/`, that can resolve as `/zh/images/example.png` and break the image.

## Publications

The Chinese `代表性成果` section should keep the same publication cards and cover images as the English `Publications` section unless there is a specific reason to differ.

For each publication card:

- Keep the same card structure: `paper-box`, `paper-box-image`, `paper-box-text`.
- Use root-based image paths with `relative_url`.
- Keep DOI, CNKI, certificate, and other external links unchanged unless the destination has changed.
- If translating titles or venues, make sure the publication identity remains clear.

## Notes And Blog Posts

The homepage note lists are language-filtered:

- English homepage Latest Notes shows `lang: en` posts and older posts with no `lang`.
- Chinese homepage 最新笔记 shows only `lang: zh` posts.

When adding bilingual versions of the same post:

- Give each version its own file in `_posts/`.
- Give each version its own `permalink`.
- Give both versions the same `translation_key`.
- Use the same `cover_image` if they are versions of the same article.
- Never give two language versions the same permalink, because one generated page can overwrite the other.
- The `/blog/` All Notes page defaults to English versions only. If an English post has a matching Chinese version, the Chinese version should be linked from the English card through `translation_key`.

Recommended permalink pattern:

```yaml
# Chinese
permalink: /blog/example/
lang: zh
translation_key: example

# English
permalink: /blog/example-en/
lang: en
translation_key: example
```

If a post only exists in English and has no `lang`, it may still appear on the English homepage as legacy content. New posts should always set `lang` explicitly.

## Build Check

Before publishing changes, run:

```bash
bundle exec jekyll build --trace
```

Then check:

- `_site/index.html` for the English homepage.
- `_site/zh/index.html` for the Chinese homepage.
- Image paths should start with `/images/`.
- English Latest Notes should not show Chinese titles.
- Chinese 最新笔记 should not show English duplicate titles.

If `Gemfile.lock` is generated locally and was not already tracked, do not add it automatically. The current repository works without committing a local platform-specific lock file.
