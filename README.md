# OT Security Field Notes

A Markdown blog for Pavithran Ganesan, using GitHub Pages and custom Jekyll layouts, with Minima retained as the base theme.

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

## Design

The responsive design lives in `assets/css/site.css`. Custom templates in `_layouts/` override the base theme: `home.html` renders the profile homepage, `articles.html` lists posts automatically, `post.html` renders articles, and `page.html` renders pages such as About. All share `default.html` for navigation, metadata, and the footer. No JavaScript or external font downloads are required. Keep using Markdown in `_posts/` to publish.

## Site sections

- `/`: personal profile and section cards, plus the latest article.
- `/articles/`: all published articles.
- `/projects/`: Projects & Labs; currently an honest empty state.
- `/about/`: author introduction.

Edit `about.md` for your biography. No employer, certifications, project achievements, or contact links have been assumed.

## Build without a system Ruby installation

If Docker is available, Ruby 3.3 can run in a container instead of being installed on the host:

```sh
docker run --rm -v "$PWD:/site" -w /site -e BUNDLE_PATH=/site/vendor/bundle ruby:3.3-bookworm sh -c 'bundle install && bundle exec jekyll build --strict_front_matter'
```

On managed cloud machines, use the managed local Docker daemon. Preserve its proxy configuration and mount the provided CA bundle read-only, setting `SSL_CERT_FILE` and `BUNDLE_SSL_CA_CERT` to its container path. Do not disable certificate verification. Dependencies remain in ignored `vendor/bundle`; generated HTML is in ignored `_site`.
