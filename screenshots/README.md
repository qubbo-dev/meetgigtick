# Screenshots

Eight screens, one per phone on the page:

| File                 | Where it shows                              |
| -------------------- | ------------------------------------------- |
| `home.webp`          | Hero, the big phone                         |
| `smart-import.webp`  | Smart Import                                 |
| `photos-found.webp`  | Memories, left phone of the pair             |
| `memories.webp`      | Memories, right phone of the pair            |
| `live.webp`          | Instant Track                                |
| `setlist.webp`       | The music                                    |
| `weather.webp`       | The rest of it, left figure                  |
| `profile.webp`       | The rest of it, right figure                 |

## Why they need no device frame

These already arrive wearing one — a device mockup on a **transparent**
background. The page adds only light around them, and `drop-shadow` follows
the real phone silhouette instead of a rectangle. Don't put them back inside
a CSS frame; you'd get two.

A raw screenshot straight off the phone would need a frame drawn for it, so
if you swap one in, either mock it up the same way first or expect it to sit
flat on the page.

## Replacing one

Keep the filename and the page picks it up. The originals live in `_source/`
(git-ignored, so they stay on your disk and out of the repo). To regenerate
the shipped copies from them:

```
python3 -c "
from PIL import Image
im = Image.open('_source/YOUR FILE.png').convert('RGBA')
w = 700; h = round(im.height * w / im.width)
im.resize((w, h), Image.LANCZOS).save('name.webp', 'WEBP', quality=82, method=6)
"
```

700px wide is 2× the largest size any phone is displayed at, and WebP keeps
the alpha channel. The eight files together come to about 540 KB — as PNG
the same set was 5.9 MB, which is why they aren't PNG.

Every phone below the hero is `loading="lazy"` and carries explicit
`width`/`height`, so nothing shifts as they arrive.
