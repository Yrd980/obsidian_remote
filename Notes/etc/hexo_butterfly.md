# 0) Prereqs (Arch/KDE/fish)

```bash
# node + git
sudo pacman -S nodejs npm git

# hexo CLI
npm i -g hexo-cli
```

> Tip: Stick to Node LTS (≥18). If you use `nvm`, pick the LTS before installing Hexo.

# 1) Create a fresh Hexo site

```bash
hexo init my-blog
cd my-blog
npm i
```

# 2) Install the Butterfly theme

Two easy ways—pick one.

**A. Clone into themes/**

```bash
git clone https://github.com/jerryc127/hexo-theme-butterfly themes/butterfly
```

**B. Git submodule (nice for updates)**

```bash
git submodule add https://github.com/jerryc127/hexo-theme-butterfly themes/butterfly
```

# 3) Install required renderers (Butterfly uses Pug & Stylus)

```bash
npm i -S hexo-renderer-pug hexo-renderer-stylus
```

# 4) Point Hexo to the theme

Edit **\_config.yml** (the root one):

```yml
# _config.yml
theme: butterfly

# recommended basics
language: en
url: https://<your-domain-or-gh-username>.github.io
permalink: :year/:month/:day/:title/
```

# 5) Make a dedicated theme config file

Butterfly ships its own `_config.yml` inside the theme. Copy it to the project root so theme options survive theme updates:

```bash
cp themes/butterfly/_config.yml _config.butterfly.yml
```

Then, at the **bottom** of your root **\_config.yml**, add:

```yml
# Merge theme config from a separate file
theme_config: ./_config.butterfly.yml
```

> Now tweak **\_config.butterfly.yml** for menus, widgets, colors, sidebar, search, etc.

# 6) Useful (optional) plugins that play well with Butterfly

```bash
# search box without external services
npm i -S hexo-generator-searchdb

# Git deploy (for GitHub Pages)
npm i -S hexo-deployer-git

# (optional) pretty permalinks
npm i -S hexo-abbrlink
```

Add to **\_config.yml** if you installed them:

```yml
# searchdb
search:
  path: search.xml
  field: post

# abbrlink (optional)
abbrlink:
  alg: crc32
  rep: hex
```

# 7) Write a post with Butterfly-friendly front-matter

```bash
hexo new post "Hello Butterfly"
```

Edit `source/_posts/hello-butterfly.md`:

```yaml
---
title: Hello Butterfly
date: 2025-08-08
tags: [intro]
categories: [Blog]
cover: /images/covers/hello.jpg     # list cover
top_img: /images/banners/hello.jpg  # page top banner
description: First post with Butterfly.
---
Your content here.
```

Put images under `source/images/...`.

# 8) Run locally

```bash
hexo clean
hexo s   # visit http://localhost:4000
```

# 9) Deploy to GitHub Pages (one-liner workflow)

```bash
# in _config.yml
deploy:
  type: git
  repo: https://github.com/<you>/<you>.github.io.git
  branch: main   # or gh-pages, match your repo setup
```

Then:

```bash
hexo g -d   # generate & deploy
```

Custom domain? Add a `source/CNAME` file with your domain (e.g., `blog.example.com`).

# 10) Updating the theme later

```bash
# if cloned
cd themes/butterfly && git pull && cd ../..

# if submodule
git submodule update --remote themes/butterfly
```

Because your options live in `_config.butterfly.yml`, updates are painless.

---

## Common “gotchas” (and quick fixes)

* **Blank page / CSS missing:** you forgot `hexo-renderer-stylus` or `hexo-renderer-pug`. Install both and `hexo clean && hexo g`.
* **Search box shows but no results:** ensure `hexo-generator-searchdb` is installed and `search:` block is in `_config.yml`, then `hexo g`.
* **Cover/top images not showing:** check paths are relative to `source/` (e.g., `source/images/...` → use `/images/...` in front-matter).
* **GitHub Pages not updating:** verify `deploy:` config, correct branch, and that the repo exists. Also check Actions settings if you rely on CI.

---

## Mental model (why these steps matter)

Think of Hexo as the engine, Butterfly as the body kit. Hexo renders markdown to HTML; Butterfly provides the layout, widgets, and styles. Renderers (Pug/Stylus) are like translators Hexo needs so Butterfly’s templates compile correctly.

---

## Deep-dive next step

Do you want:

1. a **ready-to-commit starter repo** with Butterfly + search + GH Pages wired (I can generate it), or
2. a **minimal `_config.butterfly.yml` template** tailored to a clean, fast, no-frills blog?

Pick one, and I’ll ship it.
