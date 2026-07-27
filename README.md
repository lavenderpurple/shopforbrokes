# ShopForBrokes

This folder is a complete, pre-built static website. There is nothing to
install, build, or configure — just upload it as-is.

## Files in this folder
- `index.html` — the page itself (also loads Tailwind and Leaflet from CDNs)
- `bundle.js` — the entire app (React + all the shopping logic), already
  compiled into one plain file
- `.nojekyll` — tells GitHub Pages not to run its own processing on these
  files (a standard, harmless housekeeping file)

## How to deploy on GitHub Pages

1. Go to https://github.com/new and create a new **public** repository
   (e.g. `shopforbrokes`).
2. On the new repo's page, click **"uploading an existing file"**.
3. Drag in all files from this folder — `index.html`, `bundle.js`,
   and `.nojekyll` (make sure all three end up in the repo's root, not in
   a subfolder).
4. Commit the files.
5. Go to **Settings → Pages** in that repository.
6. Under "Build and deployment," choose **Source: Deploy from a branch**,
   branch **main**, folder **/ (root)**, then **Save**.
7. Wait about a minute, then refresh that Pages settings page — it will
   show your live URL, something like:
   `https://your-username.github.io/shopforbrokes/`

When updating a file later, always replace it on GitHub by clicking
directly into that file (not "Add file → Upload files" again), otherwise
it can land in the wrong place.

## Testing locally (optional)

Because everything is a plain script (not an ES module), you can open
`index.html` directly by double-clicking it. If your browser still blocks
something, run:

```
python3 -m http.server 8000
```

from inside this folder and open `http://localhost:8000` instead.

## What this site does

Product data (titles, prices, images, sizes) is fetched live, in the
visitor's browser, from the public product catalogs of real stores
(Allbirds, Princess Polly, Beginning Boutique, Edikted, Oh Polly,
Chubbies, Taylor Stitch, Koio, ColourPop, Kylie Cosmetics, Tower 28,
Glow Recipe, MVMT, Vitaly). Products stream in progressively as each
store responds, so the page fills in gradually rather than waiting on
the slowest one. Some stores may occasionally be unreachable — the app
skips those quietly rather than showing a fake substitute.

Cart, wishlist, checkout, and order tracking are simulated in memory for
demo purposes — no real payments or orders are processed. Order tracking
now progresses realistically over the real 5-day delivery window instead
of instantly. On the Orders page, "Track on Map" optionally asks for
your browser location (used only to plot a delivery point on a free
OpenStreetMap/Leaflet map — nothing is sent anywhere or stored); if you
decline or it's unavailable, a demo location is shown instead.
