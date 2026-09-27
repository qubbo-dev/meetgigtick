# meetgigtick

The product site for **Gigtick** — the concert diary for iPhone.

Live at <https://meetgigtick.com/>

## What's here

```
index.html            the whole site — one file, no build step
assets/icon.png       app icon (square), the social preview and the favicons' source
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

- `--bg`, `--band` — the white ground and the faint lilac that every other
  section sits on (add `class="band"` to a section to put it there)
- `--ink` … `--ink-4` — text, from headings down to decoration. `--ink-3` is
  the lightest colour allowed for running text.
- `--violet`, `--rose`, `--indigo`, `--amber` — the app's own accent colours,
  taken from `AccentPalette.swift`. `--rose` is Attended, `--indigo` is
  Upcoming, `--violet` is Wishlist, and the page uses them for those three
  things only. They're too light for text on white, so each has a deepened
  `--…-ink` twin; the `.c-rose` / `.c-violet` / … classes set both, plus a
  pale tint for icon squares.
- `.card` — the white panel with its hairline and soft shadow. Change it once
  and every panel follows.
- `.panel` — the lilac stage with a violet light top left and a rose one
  bottom right. It opens the page (the hero, whose phones step out through
  its bottom edge) and closes it (the last App Store button).
- `.perf` / `.stub` — the ticket perforation and the notched stub shape used
  by the pricing cards.

**Dark mode.** Every colour that differs between light and dark is a token
in `:root`, and the **Dark** block (`:root[data-theme="dark"]`) holds its dark
value. A small script in `<head>` sets `data-theme` before the first paint: the
choice made with the moon/sun button in the nav if there is one (saved in
`localStorage`), otherwise the system setting. A new colour goes in as a token
with both values, never written straight into a rule, or it will be wrong in
one of the two themes.

Everything that moves lives in the **Motion** block near the end of the
styles: the hero assembling on load, the feature strip, the phones rising
with the scroll (CSS scroll timelines, so they only run where the browser
supports them), the icons and the pricing tickets. None of it is needed for
the page to work, and `prefers-reduced-motion` switches all of it off. One
rule to keep: don't animate anything that carries a soft gradient (the hero
washes, the glows behind the phones, the closing panel). A moving layer loses
the dithering a still one gets, and the faint gradients band into rings.

The logo itself is not `assets/icon.png` — it's a 96px copy of the icon
inlined as a data URI in the `--logo` custom property, because a relative
`<img>` doesn't resolve when `index.html` is opened straight off disk. All
three logo marks read from that one copy. To change it, regenerate the
data URI from a new icon; the PNG in `assets/` stays as the favicons' source.

The favicons (`favicon.ico` at 16/32/48 and `assets/favicon-192.png`) come
from the rounded icon exported from Affinity (`gigikonka_light v3 corners`,
kept with the design files), trimmed of the few pixels of transparent border
around the shape so it fills the square. `assets/apple-touch-icon.png` (180px)
must stay square: iOS rounds it itself and paints transparency black. When the
icon changes, regenerate all three and bump the `?v=` on both favicon links,
or browsers keep showing the old one.

Typefaces are loaded from Google Fonts: Archivo for headlines, Instrument
Sans for body text, Space Mono for anything that would be printed on a
ticket (dates, venues, prices, section labels).

## Being findable

`index.html` carries a `<link rel="canonical">` and a block of JSON-LD
describing the app (name, developer, category, the App Store link, three
screenshots). There is also a `sitemap.xml`.

**If the site ever moves to its own domain, three things must change or Google
will keep pointing at the old address:** the `canonical` link, every absolute
URL inside the JSON-LD, and the `<loc>` in `sitemap.xml`.

The JSON-LD deliberately has no `aggregateRating`. Inventing review counts is
the fastest way to get structured data ignored or penalised — add one only when
there are real numbers to quote.

There is no `robots.txt`, and one can't usefully be added: it has to sit at the
root of the domain (`qubbo-dev.github.io/robots.txt`), which belongs to a
user-site repo that doesn't exist. No robots.txt means everything is allowed,
which is what we want anyway. A custom domain would make the site the root, and
then it becomes possible.

## Keeping it honest

The page describes Gigtick 1.2. If a claim changes in the app, these are the
spots that need updating:

- **Free-tier limits** in the pricing section — they mirror `PremiumConfig`
  in the app (25 media per concert, 5 Smart Import concerts, 7 Instant
  Tracks).
- **Prices** — €2.99 monthly, €19.99 yearly, 7-day trial.
- **Version and OS** in the footer.
- The App Store link points at `id6783332108`.
