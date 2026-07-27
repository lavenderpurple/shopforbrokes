# ShopForBrokes

This folder is a complete, pre-built static website. There is nothing to
install, build, or configure — just upload it as-is.

## Files in this folder
- `index.html` — the page itself
- `bundle.js` — the entire app (React + all the shopping logic), already
  compiled into one plain file
- `.nojekyll` — tells GitHub Pages not to run its own processing on these
  files (a standard, harmless housekeeping file)

## How to deploy on GitHub Pages

1. Go to https://github.com/new and create a new **public** repository
   (e.g. `shopforbrokes`).
2. On the new repo's page, click **"uploading an existing file"**.
3. Drag in all three files from this folder — `index.html`, `bundle.js`,
   and `.nojekyll` (make sure all three end up in the repo's root, not in
   a subfolder).
4. Commit the files.
5. Go to **Settings → Pages** in that repository.
6. Under "Build and deployment," choose **Source: Deploy from a branch**,
   branch **main**, folder **/ (root)**, then **Save**.
7. Wait about a minute, then refresh that Pages settings page — it will
   show your live URL, something like:
   `https://your-username.github.io/shopforbrokes/`

That's it. Nothing else needs to be touched.

## Testing locally (optional)

Because everything is now a plain script (not an ES module), you can
open `index.html` directly by double-clicking it — no local server
required. If your browser still blocks something, run:

```
python3 -m http.server 8000
```

from inside this folder and open `http://localhost:8000` instead.

## What this site does

Product data (titles, prices, images, sizes) is fetched live, in the
visitor's browser, from the public product catalogs of real stores
(Allbirds, Princess Polly, Chubbies, ColourPop, Kylie Cosmetics, MVMT).
Cart, wishlist, checkout, and order tracking are all simulated in memory
for demo purposes — no real payments or orders are processed.
