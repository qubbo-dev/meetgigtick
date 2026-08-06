# Screenshots

Drop real App Store screenshots in here and they replace the hand-built
mockups on the page automatically. Three slots are wired up:

| File            | Where it shows                | Suggested screen                    |
| --------------- | ----------------------------- | ----------------------------------- |
| `home.png`      | Hero, the big phone           | Home tab                            |
| `concert.png`   | Smart Import section          | A concert detail with photos + setlist |
| `live.png`      | Instant Track section         | Lock Screen with the Live Activity  |

## What to export

Take them on a modern iPhone (any 19.5:9 device) and **crop off the device
bezel** — the page draws its own frame, status bar and Dynamic Island around
the image. A plain screenshot straight from the phone is exactly right.

Portrait, 9:19.5, PNG. Anything from 1170×2532 up is plenty.

## How the swap works

Each phone on the page has a `.shot` layer sitting on top of the mockup:

```html
<div class="shot" style="--shot:url('screenshots/home.png')"></div>
```

If the file exists, it paints over the mockup. If it doesn't, the CSS
resolves to nothing and the mockup underneath shows instead — so the page
never breaks, and you can add the three screenshots one at a time.

To wire up a fourth phone somewhere, copy any `.device` block in
`index.html` and point its `--shot` at a new filename.
