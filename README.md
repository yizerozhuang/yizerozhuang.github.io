# Personal Site (Jekyll + Hacker theme)

This is a GitHub Pages-ready Jekyll site using the Hacker theme with pages for Home, Blog, Photos, and Resume.

## Structure

- `index.md`: Home
- `blog/index.md`: Blog index (lists posts from `_posts/`)
- `_posts/`: Blog posts (example included)
- `photos/index.md`: Photo gallery (driven by `_data/photos.yml`)
- `_data/photos.yml`: List of photos (url, title, caption)
- `resume/index.md`: Resume page with link to `assets/resume.pdf`
- `assets/`: Static assets (e.g., resume.pdf)
- `_config.yml`: Site configuration

## Local preview

If you want to preview locally:

```bash
# Ruby + Bundler required
gem install bundler jekyll
bundle init
bundle add jekyll jekyll-seo-tag jekyll-feed
bundle exec jekyll serve --livereload
```

Open `http://localhost:4000`.

## Deploying to GitHub Pages

- Create a repository named `<username>.github.io` (user/organization site) or any repo (project site).
- Commit all files from this folder to the repository root.
- In GitHub settings → Pages, set Source to `Deploy from a branch` and choose the `main` branch.
- For project sites, set `baseurl` in `_config.yml` to `/<repo>` and access at `https://<username>.github.io/<repo>/`.

GitHub Pages supports the `jekyll-theme-hacker` theme natively, so no extra theme gem is required.

## Customize

- Update `_config.yml` `title`, `description`, and `author`.
- Replace sample post in `_posts/` with your own.
- Edit `_data/photos.yml` to add your photos.
- Drop your PDF at `assets/resume.pdf` and tweak `resume/index.md`.
