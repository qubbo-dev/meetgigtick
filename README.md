# meetgigtick

The product site for **Gigtick** — the concert diary for iPhone.

Live at <https://qubbo-dev.github.io/meetgigtick/>

## What's here

```
index.html            the whole site — one file, no build step
assets/icon.png       app icon, used for the favicon and the social preview
screenshots/          drop real app screenshots here (see its README)
.nojekyll             tells GitHub Pages to serve the files as-is
```

There is no framework, no bundler and nothing to install. Open `index.html`
in a browser and you're looking at the finished thing.

## Publishing it

Push to `main`, then in the repo: **Settings → Pages → Source: Deploy from a
branch → `main` / `root`**. First build takes a minute or two.

## Editing

Everything lives in `index.html`. The design tokens are at the very top of
the `<style>` block:

- `--room`, `--stage` — the dark ground
- `--violet`, `--rose`, `--indigo`, `--amber` — the app's own accent colours,
  taken from `AccentPalette.swift`. `--rose` is Attended, `--indigo` is
  Upcoming, `--violet` is Wishlist, and the page uses them for those three
  things only.
- `.glass` — the liquid-glass panel. Change it once and every panel follows.
- `.perf` / `.stub` — the ticket perforation and the notched stub shape used
  by the pricing cards.

The logo itself is not `assets/icon.png` — it's a 96px copy of the icon
inlined as a data URI in the `--logo` custom property, because a relative
`<img>` doesn't resolve when `index.html` is opened straight off disk. All
three logo marks read from that one copy. To change it, regenerate the
data URI from a new icon; the PNG in `assets/` stays for the favicon.

Typefaces are loaded from Google Fonts: Archivo for headlines, Instrument
Sans for body text, Space Mono for anything that would be printed on a
ticket (dates, venues, prices, section labels).

## Keeping it honest

The page describes Gigtick 1.2. If a claim changes in the app, these are the
spots that need updating:

- **Free-tier limits** in the pricing section — they mirror `PremiumConfig`
  in the app (25 media per concert, 5 Smart Import concerts, 7 Instant
  Tracks).
- **Prices** — €2.99 monthly, €19.99 yearly, 7-day trial.
- **Version and OS** in the footer.
- The App Store link points at `id6783332108`.
