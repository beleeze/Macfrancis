# Macfrancis Belchi — IT Systems Administrator portfolio

Static single-page portfolio. No build step, no dependencies to install.

## Publish on GitHub Pages

1. Create a repository (public), e.g. `macfrancis-portfolio`.
2. Commit everything in this folder to the default branch:

   ```
   git init
   git add -A
   git commit -m "Portfolio"
   git branch -M main
   git remote add origin https://github.com/<your-user>/<repo>.git
   git push -u origin main
   ```

3. In the repo: **Settings → Pages → Build and deployment**. Source: *Deploy from a branch*. Branch: `main`, folder: `/ (root)`. Save.
4. The site goes live at `https://<your-user>.github.io/<repo>/` within a minute or two.

For a root domain (`https://<your-user>.github.io/`), name the repository `<your-user>.github.io` instead.

## What must be committed

| Path | Why |
|---|---|
| `index.html` | The page itself |
| `support.js` | Runtime the page loads |
| `image-slot.js` | Photo placeholders |
| `_ds/` | Design system bundle, stylesheet and fonts |
| `assets/` | Hero background photo |
| `.nojekyll` | Required — without it GitHub Pages ignores the `_ds/` folder |
| `.image-slots.state.json` | Your dropped photos (hidden file — use `git add -A`) |

## Editing

`index.html` is a copy of `Portfolio A.dc.html`. Edit the source file, then copy it over `index.html` again before committing.

## Custom domain

Add a file named `CNAME` containing just your domain (e.g. `macfrancisbelchi.com`), then point a CNAME DNS record at `<your-user>.github.io`.
