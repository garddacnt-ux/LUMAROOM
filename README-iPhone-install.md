# Getting Lumaroom onto your iPhone as an app

Lumaroom is a single self-contained HTML file, so there's no App Store build
involved — instead it's set up as a **PWA (Progressive Web App)**. That gets
you a real home-screen icon, a full-screen window with no Safari address
bar, and offline use, without needing Xcode or a developer account.

## The catch: it needs to be *hosted*, not just opened as a file

iOS only offers "Add to Home Screen" as an installable app when the page is
loaded over `http://` or `https://` — opening the HTML file directly from
Files/AirDrop (`file://...`) still works fine for editing, but iOS won't
treat it as an installable app in that mode.

The fix is just to put these four files in one folder on any static file
host, keeping the filenames as-is:

```
LUMAROOM.html
manifest.json
sw.js
icon-192.png
icon-512.png
icon-180.png
```

Easiest free options:
- **GitHub Pages** — push the folder to a repo, enable Pages, done.
- **Netlify Drop** (netlify.com/drop) — drag the folder in, get a URL instantly.
- **Cloudflare Pages** — same idea.
- Or if you just want it on your own Wi-Fi network for testing: run
  `python3 -m http.server` in the folder and visit `http://<your-mac's-ip>:8000/LUMAROOM.html`
  from your iPhone.

## Installing on iPhone

1. Open the hosted URL in **Safari** (must be Safari, not Chrome — Chrome
   on iOS can't install PWAs).
2. Tap the **Share** button (square with an arrow).
3. Tap **Add to Home Screen**.
4. Give it a name (defaults to "Lumaroom") and tap **Add**.

From then on it launches from your home screen like any other app — full
screen, its own icon, and it'll keep working even with no signal, since the
service worker caches everything after the first load.

## What still runs 100% locally either way

Nothing about the editor itself changed in how it processes photos — all
the pixel work (blur, curves, HSL, exposure, brush tools) still happens
entirely in on-device JavaScript. Hosting the file just changes *how you
launch it*; it doesn't send anything anywhere.
