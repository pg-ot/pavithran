# OT Security Field Notes

A Markdown blog for Pavithran Ganesan, using GitHub Pages and Jekyll's Minima theme.

## Publish

1. Commit these files to the `main` branch of `pg-ot/pavithran` and push.
2. In GitHub, open **Settings → Pages → Build and deployment**.
3. Choose **Deploy from a branch**, select **main** and **/(root)**, and save.
4. Check the Pages build in GitHub Actions. Once it succeeds, the site is at `https://pg-ot.github.io/pavithran/`.

This does not require renaming your account or changing your other Pages sites. A public repository supports free Pages hosting on GitHub Free.

## Write an article

Create `_posts/YYYY-MM-DD-article-title.md`. For example:

```markdown
---
layout: post
title: "Network Segmentation in OT: Design vs Reality"
date: 2026-11-05 10:00:00 +0530
description: "An introduction to the engineering decisions behind OT segmentation."
categories: [OT-Cybersecurity, IEC62443]
---

Write your article here using Markdown.
```

Use the actual publication date: future-dated posts remain hidden until a build runs after that date. Commit and push the file; GitHub Pages rebuilds the article list automatically. The first article is included in `_posts/2026-11-05-the-plant-is-running-firewall-open.md`.

Store images in `assets/images/` and use paths that respect the project prefix:

```liquid
![Diagram description]({{ '/assets/images/diagram.png' | relative_url }})
```

## Local development

Install Ruby 3.1 or newer, its development headers, a compiler toolchain, and Bundler. From this checkout:

```sh
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll build --strict_front_matter
bundle exec jekyll serve --host 0.0.0.0 --port 4000
```

The project path is `/pavithran/`, including in local requests. Generated output and local dependencies are ignored by Git. Keep `Gemfile.lock` if generated to pin the local dependency versions.

## Move to another Pages address

For a personal-site repository such as `g-pavithran/g-pavithran.github.io`, set `url` to `https://g-pavithran.github.io` and `baseurl` to `""` in `_config.yml`. Update these README instructions to match. Do this only when moving the site.
