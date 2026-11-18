# Sarayu M & Shanmukhananda JM — Wedding Invitation Website

A single-file animated wedding invitation for **Sunday, 22 November 2026** at
**Shri Guru AC Function Hall, Ballari, Karnataka**.

Everything — markup, styles, artwork (SVG) and animation — lives inside
`index.html`. No build step, no framework, no dependencies. Open it in a browser
and it works; drop it on any host (Netlify, Vercel, GitHub Pages, Hostinger, a
plain Apache folder) and it works there too.

---

## 1. What's inside

```
wedding-website/
├── index.html                 ← the entire site (HTML + CSS + JS inline)
├── README.md                  ← this file
└── assets/
    └── photos/
        ├── README.txt
        └── (01.jpg … 20.jpg, vasanth.jpg  ← you add these)
```

`index.html` is self-contained: the only external request is the Google Fonts
stylesheet. If it can't load, the page falls back to Georgia / Brush Script /
system UI and still looks correct.

---

## 2. The experience

| Moment | What happens |
| --- | --- |
| **Entry gate** | A 3D invitation card floats and tilts toward the cursor. Gold script names, a blooming lotus, the date. **A tap anywhere on the screen opens it** — the “Tap to Open” pill is just the visual cue (Enter / Space work too). |
| **Shower** | Flowers rain down, balloons rise, one confetti burst. The whole thing runs for **three seconds** and clears itself, so nothing ever covers the page while guests read. |
| **Hero** | `SARAYU M & SHANMUKHANANDA JM` rises letter by letter in gold foil Cinzel, ambient petals drift behind. |
| **Countdown** | Days / hours / minutes / seconds to `11:45 AM` on 22 Nov 2026, ticking every second. |
| **Story** | Four beats, 2016 → 2019 → 2025 → 2026. |
| **Functions** | Four cards — Mehendi, Haldi, Muhurtham, Reception — each with its own accent colour, emoji and **View on map** link. Cards tilt in 3D under the cursor with a moving glare. |
| **Gallery** | 20 frames in a masonry-ish grid; click any frame for a full-screen lightbox with caption and arrow-key navigation. |
| **Interlude** | Gold lotus + two rose rosettes and a blessing. |
| **Venue** | Address card, plus-code, an animated SVG map panel and two buttons: *Open in maps* and *Get directions*. |
| **Footer** | Contact strip (`76764 61604`, tap to call), watermark wordmark, and **Made with ♥ by Vasanth** → opens a credit card. |

Also included: scroll progress bar, sticky pill navigation, back-to-top,
light/dark theme toggle (remembered in `localStorage`), “Add to calendar”
(downloads `Wedding-Functions-2026.ics` with all four functions), full keyboard
focus rings, and `prefers-reduced-motion` support that switches the animation off.

---

## 3. Add the photos (5 minutes)

1. Rename 20 couple photos to `01.jpg` … `20.jpg`.
2. Copy them into `assets/photos/`.
3. Reload. Frames light up as the files load; each keeps its caption and its
   size hint, so the grid stays balanced.

Missing files are handled gracefully — the frame shows its number and
“PHOTO” label instead of a broken image, so the site never looks broken while
you're still collecting pictures.

Sizing tip: **1600 px on the long edge, JPEG quality ~78** keeps the whole album
under ~4 MB. Photography is the one thing that should be compressed.

---

## 4. Edit the content

Open `index.html`, find the `CONFIG` object near the top of the `<script>`
(step 1 of 17). Everything the family might change lives there:

```js
const CONFIG = {
  bride:  "Sarayu M",
  groom:  "Shanmukhananda JM",
  hashtag:"#SarayuWedsShanmukhananda",
  weddingISO:   "2026-11-22T11:45:00+05:30",   // countdown target
  muhurthamEndISO:"2026-11-22T12:15:00+05:30", // when the countdown retires
  venue: { name, lines, plusCode, mapUrl, directionsUrl },
  contact: { label:"For any details", phone:"7676461604" },
  credit:  { name:"Vasanth", instagram, instagramUrl, email, photo },
  events: [ mehendi, haldi, muhurtham, reception ],
  story:  [ 4 entries ],
  photos: [ 20 entries ]
};
```

Change a value, save, reload. Nothing else needs touching.

### Things to replace before you share the link

| Where | What | Why |
| --- | --- | --- |
| `CONFIG.credit.instagram` | `"@vasanth"` | Placeholder handle |
| `CONFIG.credit.instagramUrl` | `"https://instagram.com/"` | Placeholder link |
| `CONFIG.credit.photo` | `assets/photos/vasanth.jpg` | Add the picture or the modal shows initials |
| `CONFIG.events[0].time` / `[1].time` | `"Time to be announced"` | Mehendi & Haldi timings weren't final at hand-off |
| `assets/photos/01–20.jpg` | — | The twenty photos |

If `CONFIG.credit.email` is left empty, the credit card's contact button falls
back to the family phone number.

---

## 5. Dates & times already wired in

| Function | Date | Time |
| --- | --- | --- |
| Mehendi 🌿 | Thursday, 19 Nov 2026 | to be announced |
| Haldi 🌼 | Friday, 20 Nov 2026 | to be announced |
| Muhurtham 💍 | Sunday, 22 Nov 2026 | 11:45 AM – 12:15 PM |
| Reception 🎊 | Sunday, 22 Nov 2026 | 1:00 PM onwards |

The countdown counts to **11:45 AM**. Between 11:45 and 12:15 it reads
*“The muhurtham is underway.”* After 12:15 it switches permanently to the
*“a new beginning begins”* state — no negative numbers, ever.

---

## 6. Design notes

- **Palette** — charcoal `#101216`, sand `#EBE0CA`, electric blue `#2E6BFF`, with
  gold foil `#E5C158` and rose `#E29BB0` as accents. The light theme swaps
  charcoal for warm ivory `#F7F3EB`; the blue stays the same, so the identity
  survives the toggle.
- **Type** — Cinzel (display), Great Vibes (script), Bricolage Grotesque
  (eyebrows, buttons, nav), Outfit (body). Loaded from Google Fonts; local
  fallbacks are declared for every role.
- **Artwork** — the lotus, roses, map panel and every icon are inline SVG, so
  they stay crisp at any size and add no image weight.
- **Emoji** — used only on the four function cards, as quiet colour markers.
  Everything else is typographic, so the page reads as an invitation rather
  than a group chat.
- **Motion budget** — canvas layers cap their device-pixel-ratio at 2, particle
  counts scale with viewport width, and both the shower and the confetti run on
  the wall clock: three seconds, then they are gone — even on a phone that
  drops frames.

---

## 7. Sharing it

Upload the folder as-is. For a link that previews nicely when sent on WhatsApp,
add these tags inside `<head>` (they're safe to drop in):

```html
<meta property="og:title" content="Sarayu M & Shanmukhananda JM — 22 Nov 2026">
<meta property="og:description" content="Join us at Shri Guru AC Function Hall, Ballari.">
<meta property="og:image" content="https://your-site.com/assets/photos/01.jpg">
<meta property="og:type" content="website">
```

A custom domain, e.g. `sarayu-shanmukhananda.in`, costs about ₹500–800/year and
makes the invitation feel like a keepsake rather than a file.

---

Made with ♥ by **Vasanth**
