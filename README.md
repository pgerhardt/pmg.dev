# pmg.dev

Hugo site. Built on push → GitHub Actions → `gh-pages` → served at **https://pmg.dev**.

## Workflow

- **Do edit:** Markdown sources in `content/`  
- **Don’t edit:** generated static files in `public/` (ignored; built by CI)

```
content/            # your pages/posts (.md)
assets/css/extended # custom CSS (e.g. reader.css)
layouts/            # template overrides (optional)
static/CNAME        # pmg.dev (copied into build)
themes/PaperMod     # theme (git submodule)
.github/workflows   # Pages deploy workflow
hugo.yaml           # site config
public/             # build output (generated)
```

## Local dev

```bash
hvm use 0.146.0
hugo server -D
# open http://localhost:1313
```

## Edit → Deploy

```bash
# edit content
$EDITOR content/_index.md   # or any content/*.md

# commit + push
git add -A
git commit -m "update"
git push
```

GitHub Actions builds with pinned Hugo and publishes to `gh-pages`. No manual copy to `public/`.

## Building manually (rare)

```bash
hugo --minify         # outputs to ./public (do not commit)
```

## Styling / layout

- CSS: `assets/css/extended/reader.css`  
- Theme params: `hugo.yaml` under `params:`  
- Template overrides: put files in `layouts/` to override theme partials/templates (e.g., `layouts/partials/footer.html`, `layouts/index.html`)

## Hosting

- Custom domain is baked via `static/CNAME` (contains `pmg.dev`)
- GitHub Pages: **Settings → Pages → Source = Deploy from a branch → gh-pages / (root)**
- DNS points `pmg.dev` → GitHub Pages (via Cloudflare)

## Common ops

- **Redeploy without changes**
  ```bash
  git commit --allow-empty -m "redeploy"
  git push
  ```
- **Revert last N commits (safe)**
  ```bash
  git revert --no-edit HEAD~(N-1)..HEAD
  ```

## Notes

- Do **not** commit `public/`.
- Content lives in `content/*.md`. (If you keep drafts elsewhere, move/rename into `content/` to publish.)
- Any per-page front matter uses YAML/TOML front matter at the top of the `.md`.
