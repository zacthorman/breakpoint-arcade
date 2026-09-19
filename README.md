# Breakpoint Arcade

A small app for learning to read and write code, by reading listings, drilling
the shapes, and then breaking six browser games that were built to be broken.

Three tasks a day, a streak that resets if you miss one, and every round
regenerated with new numbers so you can't memorise your way through it.

**Live version:** https://ZDTHORMAN.github.io/breakpoint-arcade/
*(this link works once you've done the Pages step below)*

---

## What's in here

| File | What it is |
|---|---|
| `index.html` | The entire app — HTML, CSS and JavaScript in one file. No build step, no dependencies. |
| `manifest.webmanifest` | Tells phones and desktops it can be installed as an app: name, icon, colours. |
| `sw.js` | The service worker. Caches the app so it opens with no signal. |
| `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` | App icons. |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are, without trying to build a blog out of them. |

Everything you do is stored in your own browser (`localStorage`). Nothing is
sent anywhere, there is no account, and there is no server.

---

## Putting it on GitHub (about five minutes)

1. Go to **github.com/new**.
2. Repository name: `breakpoint-arcade`. Set it to **Public** — GitHub Pages
   needs public on a free plan. Don't tick "add a README", you already have one.
3. Click **Create repository**.
4. On the empty repo page, click **uploading an existing file**.
5. Open this folder in Finder, select **all the files inside it** (not the
   folder itself) and drag them into the browser window. Make sure hidden files
   are showing first — press `Cmd + Shift + .` in Finder — so `.nojekyll`
   comes along too.
6. Click **Commit changes**.
7. Go to **Settings → Pages** (left-hand menu).
8. Under "Build and deployment", set Source to **Deploy from a branch**,
   branch **main**, folder **/ (root)**. Click **Save**.
9. Wait a minute or two, then open
   `https://ZDTHORMAN.github.io/breakpoint-arcade/`.

If you get a 404, give it another minute — the first deploy is the slow one.

## Installing it as an app

**iPhone / iPad:** open the URL in Safari (it must be Safari), tap the Share
button, then **Add to Home Screen**. It gets its own icon and opens without any
browser chrome.

**Mac / Windows, Chrome or Edge:** open the URL and click the install icon at
the right-hand end of the address bar, or menu → Cast, Save and Share → Install.

Once installed it works with no internet. The first launch needs a connection;
after that the service worker serves it from the cache.

## Changing it later

`index.html` is the whole app. Edit it, commit, and Pages redeploys in about a
minute.

One catch: the service worker caches things. The page itself is fetched from the
network first, so a normal reload picks up your changes — but if an icon or the
manifest changes, bump the version at the top of `sw.js`:

```js
const CACHE = "bpa-v2";   // was bpa-v1
```

That makes every device throw away the old cache and refetch.

## Running it without GitHub

Double-click `index.html`. Everything works except the offline caching, which
needs a real web address. Handy for testing an edit before you commit it.

## A note on your progress

Progress is stored per web address. The copy in Claude and the copy on GitHub
Pages each keep their own streak, XP and flashcard record — they're separate
browsers' worth of storage as far as the web is concerned. Pick one as your real
one. The GitHub one is the better bet: it's yours, it's on your phone, and it
doesn't depend on anything else staying put.
