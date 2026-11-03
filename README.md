# Tha Carter Studios — website

Live at **https://1stfloorproductions.github.io/thacarterstudios/**
Share card (QR) at **https://1stfloorproductions.github.io/thacarterstudios/qr/**

Built and maintained by First Floor Productions. One page, no build step, no framework.

---

## What's in here

```
index.html            the whole site
404.html              wrong-door page
assets/
  og.jpg              1200x630 social preview
  brand/              wordmark, monogram, 24/7 mark (SVG)
  fonts/              Carter Black + Carter Caps (woff2)
  photos/             17 studio photos, each at 800px and 1600px
qr/
  index.html          the share-card app (installs to a phone home screen)
  manifest.webmanifest, sw.js, icon-*.png
  carter-black.woff2, carter-caps.woff2   (copies, so the app works offline)
```

## Updating it

Drag the changed file into GitHub (`Add file` → `Upload files`) and commit. Pages
redeploys in a minute or two. No CLI, no tokens.

### Swapping a photo
Drop a new pair into `assets/photos/` named `whatever-800.jpg` and `whatever-1600.jpg`,
then point the `src`/`srcset` of the figure at them. Keep both sizes — the grid loads the
800 and the lightbox loads the 1600.

### Changing the rate
One flat rate, $45 an hour, any room. Confirmed by Sean 2026-11-02. It lives in `index.html` in
two places that must stay in step: the `RATE` constant in the script, and the `$45` printed in the
`.rate-big` block and the `#subline` fallback text.

Everything else — engineer, mixing, mastering, video, photo days — is quoted per session and
deliberately carries no number on the page. Do not invent one. The earlier build had made-up room
rates and add-on prices; they were removed on 2026-11-02 because the site is live to real clients.

### Changing the contact details
Sean's phone and email appear in: the nav button, the contact plate, the booking mailto,
the footer, the JSON-LD block at the bottom, and the QR codes in `qr/index.html`.
Search for `6462002089` and `thacarterstudios@gmail.com` to catch them all.

## The booking form

There is no back end on GitHub Pages, so nothing can be posted anywhere. The form builds
a `mailto:` and opens the visitor's own mail app with every field filled in. That way a
request can never silently vanish into a server that was never listening.

To take submissions directly instead, point the form at Formspree, Netlify Forms, or
Sean's Calendly and delete the mailto block in the submit handler.

## The QR share card

`qr/` is a small installable app. Open it on a phone, Add to Home Screen, and it behaves
like a native app: full screen, works with no signal, keeps the screen awake while someone
is scanning. Tap the code to blow it up to full screen.

Five codes: website, Instagram, call, email, and a contact card that saves Sean straight
into the scanner's phone.

Each code is stored as a bitmap, not generated at runtime: `n` is how many modules per
side, `d` packs the grid four pixels to a hex digit, row by row. Nothing is fetched, so
they draw instantly and work offline. **If you change what a code points at, you have to
re-encode it** — editing the `url` string alone changes the caption and the share button
but not the actual code.

## Custom domain, later

When Sean pays for his own domain, add a `CNAME` file with the domain in it and point the
DNS at GitHub. Then update the absolute URLs: `og:image`, `og:url`, `canonical`, the
JSON-LD `url` and `image`, and re-encode the website and contact QR codes in `qr/`.
No rebuild needed beyond that.
