# Adda Music — public site

Served by GitHub Pages at **https://veyrastudio3192-mj.github.io/adda-music-site/**

This repo is public on purpose and holds only two kinds of thing. The app's
source lives in the private `adda-music` repo.

## `overrides.json` — the live track list

The app fetches this on launch. Editing it adds or removes songs across every
install **without a Play Store release**.

```json
{
  "version": 2,
  "blocked": ["dQw4w9WgXcQ"],
  "replace": { "deadVideoId": "workingVideoId" },
  "add": { "truck": [
    { "title": "…", "artist": "…", "youtubeId": "…", "lang": "hindi" }
  ] }
}
```

- `blocked` — gone everywhere. The takedown list, applied last so nothing can
  put a blocked id back on screen.
- `replace` — old id to new id, for a video that died. Keeps the title, artist
  and running order.
- `add` — keyed by scene id: `truck`, `highway`, `chai`, `dhaba`, `safar`,
  `baarish`, `90s`, `rooftop`, `pyaar`, `masti`.

**Bump `version` on every publish.** A running app rebuilds its scene list when
the version changes; leave it the same and an already-open app keeps the old one.

A failed fetch never un-blocks anything: the last document that arrived is
cached on the device and stays in force until a successful fetch replaces it.

Edit `docs/overrides.json` in the private repo, run `tools/make_site.py`, and
push here — that way the file the app reads is the same file its unit tests
parse.

## The pages

`index.html`, `privacy.html`, `terms.html`, `copyright.html`, `youtube.html` are
**generated** from `app/src/main/assets/content/legal.json` in the private repo.
Do not edit them here — the change would be overwritten, and the hosted policy
would disagree with the one inside the app, which is exactly the drift the
generator exists to prevent.

To change any of them: edit `legal.json`, run `python3 tools/make_site.py`, push.
