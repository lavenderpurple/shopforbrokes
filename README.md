# ShopForBrokes

This folder is a complete, pre-built static website. There is nothing to
install, build, or configure — just upload it as-is.

## Files in this folder
- `index.html` — the page itself (also loads Tailwind and Leaflet from CDNs)
- `bundle.js` — the entire app (React + all the shopping logic), already
  compiled into one plain file
- `favicon.svg`, `favicon.ico`, `favicon-16x16.png`, `favicon-32x32.png`,
  `favicon-192x192.png`, `favicon-512x512.png`, `apple-touch-icon.png`,
  `site.webmanifest` — the browser tab icon, in every size/format modern
  and legacy browsers look for (including a home-screen icon on phones)
- `.nojekyll` — tells GitHub Pages not to run its own processing on these
  files (a standard, harmless housekeeping file)

## How to deploy on GitHub Pages

1. Go to https://github.com/new and create a new **public** repository
   (e.g. `shopforbrokes`).
2. On the new repo's page, click **"uploading an existing file"**.
3. Drag in **every file** from this folder (all the favicon files too —
   `index.html` references them by name, so they need to be present)
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
visitor's browser, from the public product catalogs of 21 real stores,
spanning:
- Global/US brands: Allbirds, Princess Polly, Beginning Boutique,
  Edikted, Oh Polly, Chubbies, Taylor Stitch, Koio, ColourPop, Kylie
  Cosmetics, Tower 28, Glow Recipe, MVMT, Vitaly
- Real Indian D2C brands: mCaffeine, GIVA, Neemans, Libas, Noise,
  Urban Monkey, French Crown

Products stream in progressively as each store responds. Every price is
converted to one canonical figure internally, then displayed in whichever
currency you pick with the **$/₹ toggle** in the header (next to the
wishlist icon) — so it's always consistent, not tied to whatever
currency a given store happens to price in natively.

Note on Meesho/Myntra/Nykaa/Newme: those platforms don't expose a
public product feed the way Shopify stores do, and they run anti-bot
protection that blocks this kind of request — so they can't be
included the same way. The Indian brands above are genuinely real,
live Shopify storefronts instead.

Cart, wishlist, checkout, and order tracking are simulated in memory for
demo purposes — no real payments or orders are processed. Order tracking
progresses realistically over a real 5-day simulated delivery window. On
the Orders page, "Track on Map" optionally asks for your browser location
(used only to plot a delivery point on a free OpenStreetMap/Leaflet map —
nothing is sent anywhere or stored); if you decline or it's unavailable,
a demo location is shown instead.

Sorting (price, discount, newest) and filtering (price range, brand,
in-stock only) are available above the product grid.

**Reels** — tap the Reels button in the header (or menu on mobile) for a
full-screen, swipe-through product feed. Double-tap (or double-click) an
image to add it to your wishlist, with a heart animation like short-video
apps use. A "View Details" button on each card opens the full product
page, and going back returns you to the same spot in Reels rather than
resetting to the shop grid.

Reels also personalizes what comes next as you scroll, based on two
signals: what you've wishlisted (a strong, explicit signal) and how long
you linger on a product before scrolling past (a weaker, implicit signal —
the same basic idea short-video feeds use). Either signal alone is enough
to start personalizing; with neither yet, it stays close to the original
order. Only upcoming, not-yet-seen products are ever reordered — whatever
you've already scrolled past stays put, so the feed doesn't shuffle under
you mid-scroll. A "✨ For You" badge appears on products the algorithm
is confident about, and a small amount of randomness is mixed in so it
doesn't lock into a total filter bubble.
