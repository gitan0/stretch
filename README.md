# Stretch

A small offline PWA for guided stretching, warm-up and core routines. One `index.html`, a `manifest.json`, a service worker and three icons. No build step, no backend, no libraries.

## Edit the routines

Everything lives in the `ROUTINES` array near the top of the `<script>` in `index.html`. Each move has `name`, an optional `cue`, optional `equipment` (a string, or `{ gym, home }`), and either `reps` or `seconds`. Add `sets` for multiple sets and `eachSide: true` for a left step, a 5 second switch screen and a right step. Routines with `setting: 'gym'` or `setting: 'home'` only show for that setting.

The avoid list is the `AVOID` array just below it.

After changing any file, bump `CACHE` in `sw.js` (for example `stretch-v2`) so installed phones pick up the new version.

## Run locally

```bash
python3 -m http.server 8765 --directory /Users/luke/stretch
```

Then open http://localhost:8765 in a browser.

## Deploy to GitHub Pages

1. Create an empty repository on GitHub called `stretch` (public, no README).
2. In this folder:

```bash
cd /Users/luke/stretch && git init -b main && git add index.html manifest.json sw.js icons README.md && git commit -m "Stretch PWA" && git remote add origin https://github.com/YOUR_USERNAME/stretch.git && git push -u origin main
```

3. On GitHub open the repository, then Settings, then Pages. Under Build and deployment set Source to "Deploy from a branch", pick `main` and `/ (root)`, and save.
4. Wait a minute, then open `https://YOUR_USERNAME.github.io/stretch/` on your iPhone in Safari.
5. Tap the Share button, then "Add to Home Screen", then Add. Open it once from the home screen while online so the service worker caches the app and fonts. After that it works offline.

To ship an update: edit, bump `CACHE` in `sw.js`, then

```bash
cd /Users/luke/stretch && git add -A && git commit -m "Update routines" && git push
```

On the phone, close the app fully and reopen it twice. The first open fetches the new version in the background, the second shows it.
