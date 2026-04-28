# Content Maintenance Guide

This site uses two static homepage pages instead of a translation plugin:

- English homepage: `_pages/about.md`, served at `/`
- Chinese homepage: `_pages/about.zh.md`, served at `/zh/`

Follow the rules below when adding or updating content.

## Repository Map

Common files and folders:

- `_pages/about.md`: English homepage.
- `_pages/about.zh.md`: Chinese homepage.
- `_pages/blog.md`: All Notes index page.
- `_posts/`: note/blog post source files.
- `_data/navigation.yml`: English top navigation.
- `_data/navigation_zh.yml`: Chinese top navigation.
- `images/`: homepage images, publication images, and blog covers.
- `assets/`: CV, fonts, JavaScript, and CSS assets.
- `assets/css/accent-enhancements.css`: most custom homepage/card/blog styling.
- `.github/workflows/jekyll.yml`: GitHub Pages deployment workflow.
- `_site/`: generated output; do not edit manually.

## Language Rules

- Every page or post that has a language version must set `lang`.
- Use `lang: en` for English content.
- Use `lang: zh` for Chinese content.
- Do not rely on `site.active_lang` or `jekyll-polyglot`; this site does not use Polyglot.
- The top navigation detects language from `page.lang`.
- English is the default language via `default_lang: "en"` in `_config.yml`.

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
- Keep the homepage `permalink` values unchanged: `/` for English and `/zh/` for Chinese.
- Keep `author_profile: true` unless the page should intentionally hide the sidebar profile.

Current important anchors:

- English: `about-me`, generated heading anchors for `News`, `Publications`, `Education`, `Teaching`, `Funding & Honors`, `Notes`
- Chinese: `about-me`, `news`, `publications`, `education`, `teaching`, `notes`

Useful homepage classes:

- `accent-text`: inline emphasis in paragraphs and list items.
- `primary-gradient-text`: emphasized institution or organization names.
- `quote-accent`: short highlighted statements.
- `highlight-blocks` and `highlight-block floating-card`: homepage research-interest cards.
- `paper-box floating-card`: publication/software cards.
- `btn-accent`: DOI, CNKI, certificate, and other action links.
- `local-blogs-section`: Latest Notes section on the homepages.

Avoid changing these class names unless you also update the CSS.

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

### Cover Image Rules

Use one cover image for each note or publication card unless the content truly needs a separate visual.

File rules:

- Store cover images in `images/`.
- Use lowercase, descriptive, hyphenated filenames.
- Prefer `.png` for diagrams, screenshots, and generated illustrations.
- Prefer `.jpg` or `.jpeg` only for photo-like images.
- Use names that match the article or project slug, for example `blog-stata-ai.png` or `reits-network-lstm.png`.
- For bilingual versions of the same note, use the same `cover_image` in both posts.

Recommended dimensions:

- Blog cover images should work well in a horizontal card crop.
- Use a 16:9 or near-16:9 image when possible, such as `1200x675`, `1600x900`, or `1920x1080`.
- Keep important text, logos, and diagrams away from the edges because cards use `object-fit: cover`.
- Do not rely on small text inside the image; titles are already shown in the card.

Visual style:

- Covers should reveal the topic directly, not just use abstract decoration.
- For technical tutorials, use a clear workflow, tool interface, or concept diagram.
- For academic outputs, use a clean research-style diagram or topic-relevant visual.
- Avoid overly dark, blurry, cropped, or generic stock-like images.
- Avoid one-note decorative gradients, random blobs, or purely atmospheric backgrounds.

Front matter example:

```yaml
cover_image: "/images/blog-example-topic.png"
```

Publication card example:

```html
<img src="{{ '/images/example-publication.png' | relative_url }}" alt="Short descriptive alt text">
```

Before publishing:

- Confirm the image file exists in `images/`.
- Confirm the generated HTML path starts with `/images/`.
- Check both `_site/index.html` and `_site/zh/index.html` when the image appears on both homepages.
- Check `_site/blog/index.html` for blog covers.

## Publications

The Chinese `代表性成果` section should keep the same publication cards and cover images as the English `Publications` section unless there is a specific reason to differ.

For each publication card:

- Keep the same card structure: `paper-box`, `paper-box-image`, `paper-box-text`.
- Use root-based image paths with `relative_url`.
- Keep DOI, CNKI, certificate, and other external links unchanged unless the destination has changed.
- If translating titles or venues, make sure the publication identity remains clear.
- Badges should be short status labels, for example `Published`, `Published · ACM`, `Peer Review · JCR Q1`, or `Minor Revision · JCR Q1`.
- Use Font Awesome icons already used in the site for action buttons, such as `fa-link` for DOI/CNKI and `fa-certificate` for certificates.
- Certificate or local image links should also use root-based paths, for example `/images/sw1.png`.

Minimal publication card template:

```html
<div class='paper-box floating-card'>
  <div class='paper-box-image'>
    <div class="badge pulse-accent">Published</div>
    <img src="{{ '/images/example-publication.png' | relative_url }}" alt="Short descriptive alt text">
  </div>
  <div class='paper-box-text'>
    <h3>Publication title</h3>
    <div class="authors"><strong>Yanying Wei</strong>, Coauthor Name</div>
    <div class="venue"><em>Journal or Proceedings</em>, year, volume(issue): pages.</div>
    <div class="links">
      <a href="https://doi.org/example" class="btn-accent"><i class="fas fa-link"></i> DOI</a>
    </div>
  </div>
</div>
```

## Notes And Blog Posts

The homepage note lists are language-filtered:

- English homepage Latest Notes shows `lang: en` posts and older posts with no `lang`.
- Chinese homepage 最新笔记 shows only `lang: zh` posts.
- The `/blog/` All Notes page defaults to English posts and legacy posts only.
- A Chinese version appears from the English card through a `中文版本` link when both posts share the same `translation_key`.

Post file rules:

- Put posts in `_posts/`.
- Use the Jekyll filename format `YYYY-MM-DD-slug.md`.
- Keep slugs lowercase and hyphenated.
- New posts should include `layout: post`, `title`, `date`, `description`, `cover_image`, `permalink`, and `lang`.
- Use `original_url` only when the post is a republication or summary of an external original source.
- Use `categories` only when you want the post template to show category metadata.

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

Full front matter template:

```yaml
---
layout: post
title: "English title"
date: 2026-04-28
description: "One-sentence summary for cards and previews."
cover_image: "/images/blog-example-topic.png"
permalink: /blog/example-en/
lang: en
translation_key: example
categories:
  - research-notes
original_url:
---
```

Post body image paths:

- The post layout normalizes `src="images/..."`
  and `href="images/..."` to `/images/...`, but still prefer writing root-based paths manually.
- Homepage Markdown does not get that same post-layout normalization, so homepage images must always use root-based paths.

## Styling Rules

Most custom visual rules live in `assets/css/accent-enhancements.css`.

When adding content:

- Prefer reusing existing classes over adding new inline styles.
- Keep card structures consistent so existing responsive CSS continues to work.
- Do not nest cards inside cards.
- Keep button labels short.
- Use existing icons from Font Awesome when possible.
- Check mobile rendering if a title is long, especially in blog cards and publication cards.
- Do not put important information only inside an image; keep the text in HTML too.

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
- `_site/blog/index.html` should show English All Notes cards and Chinese links only where available.
- If you changed navigation, click the generated links or inspect `_site/index.html` and `_site/zh/index.html`.

If `Gemfile.lock` is generated locally and was not already tracked, do not add it automatically. The current repository works without committing a local platform-specific lock file.

## Deployment And Generated Files

GitHub Pages is deployed by `.github/workflows/jekyll.yml` on pushes to `main` and `i18n-polyglot-experiment`.

Do not edit generated output directly:

- Do not edit `_site/`; edit source files instead.
- Do not commit `_site/`, `.sass-cache/`, `.bundle/`, `vendor/`, `.DS_Store`, or local-only helper files.
- If a local build creates `Gemfile.lock`, leave it untracked unless the project intentionally switches to a committed lockfile.
- The workflow runs `bundle install` and `bundle exec jekyll build --trace --verbose`.

## Common Pitfalls

- `/zh/` 404 usually means the Chinese homepage was not generated or deployed. Check `_pages/about.zh.md`, its `permalink: /zh/`, and the GitHub Actions build.
- Chinese page images missing usually means the source used `images/...` instead of `/images/...` or `relative_url`.
- English and Chinese posts overwriting each other usually means both versions share the same `permalink`.
- Chinese navigation missing usually means the data file name or Liquid reference is wrong; use `_data/navigation_zh.yml` and `site.data.navigation_zh.main`.
- Language switching wrong usually means `page.lang` is missing or incorrect.
- Duplicate notes on `/blog/` usually means the All Notes filter was changed or a bilingual post is missing `lang`.
