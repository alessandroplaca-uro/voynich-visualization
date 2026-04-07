# How to deploy on GitHub Pages

Three steps. Takes ~2 minutes and no paid account.

## Step 1 — Create the public repo on GitHub

1. Go to <https://github.com/new>
2. Fill in:
   - **Owner**: `alessandroplaca-uro`
   - **Repository name**: `voynich-visualization`
   - **Description** (optional): `Interactive 3D visualization of the Voynich morphemic system — Currier hand edition`
   - **Visibility**: ⚠️ **Public** (must be public for free Pages)
   - **Initialize this repository with**: leave everything OFF.
3. Click **Create repository**.

## Step 2 — Upload the files

Drop the 5 files (`index.html`, `README.md`, `LICENSE`, `DEPLOY.md`,
`.nojekyll`) into the repo via the web upload page:

<https://github.com/alessandroplaca-uro/voynich-visualization/upload/main>

Commit message: `Initial deploy`. Click **Commit changes**.

## Step 3 — Enable GitHub Pages

1. Go to <https://github.com/alessandroplaca-uro/voynich-visualization/settings/pages>
2. Under **Build and deployment** → **Source**: choose **Deploy from a branch**
3. **Branch**: `main`, **Folder**: `/ (root)`
4. Click **Save**.
5. Wait 30-60 seconds. When you see the green banner "Your site is live at..."
   it is ready.

The URL will be: <https://alessandroplaca-uro.github.io/voynich-visualization/>

## Notes

- The (empty) `.nojekyll` file tells GitHub Pages NOT to process the site
  with Jekyll. Required for files/folders starting with `_`.
- The HTML is self-contained: ~92 KB with all data embedded. Plotly is
  loaded from the CDN on first access.
- No backend, no DB, no API keys. It is a fully static site.
