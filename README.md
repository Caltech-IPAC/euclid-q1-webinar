# Euclid Q1 Webinar Series

Landing page for the ENSCI/IPAC webinar series walking through Euclid's Q1 data release.

This repo is **private**. Only the `/docs` folder is published to GitHub Pages — everything outside `/docs` (this README, internal notes, drafts) stays private to the repo.

## Where the live site lives

- **Source**: `docs/index.html` (+ `docs/styles.css`) on the `main` branch of `IPAC-SW/Euclid-q1-webinar`
- **Published URL**: <https://automatic-couscous-v3grz5w.pages.github.io/>
- **Linked from**: [euclid.caltech.edu](https://euclid.caltech.edu/) — the published URL above gets posted there once we're ready to launch.

> The random `automatic-couscous-…` subdomain is GitHub's standard URL pattern for Pages served from a **private** repo. The site is fully public (anyone with the link can view, no GitHub auth needed); the obscured slug just keeps the underlying private-repo's existence from being guessable. Don't bother trying to make the URL prettier — that's the format Enterprise/Team Pages uses for private sources, and there's no rename option short of making the repo public.

## How GitHub Pages deploys

1. Push to `main`.
2. GitHub Pages is configured to build from the `/docs` folder on `main` (Settings → Pages → Source: `main` / `/docs`).
3. Site is live in roughly 1 minute. No build step, no Actions, no Jekyll config needed.

There is no toolchain. Open `docs/index.html` directly in a browser to preview locally, or run a static server from the repo root:

```
python3 -m http.server 8000 --directory docs
# then open http://localhost:8000/
```

## Stack

Vanilla HTML + CSS only. No JS framework, no `package.json`, no dependencies, no build. If you find yourself wanting to add any of those, stop and check first.

## Swapping in a YouTube ID

Each unreleased video has a `TBD_*_ID` placeholder in [docs/index.html](docs/index.html). When a video is uploaded to YouTube, grab the 11-character ID from the URL (e.g. `dQw4w9WgXcQ` from `https://www.youtube.com/watch?v=dQw4w9WgXcQ`) and replace the placeholder.

Placeholders, by section:

| Section | Placeholder | Presenter |
| --- | --- | --- |
| 1. Overview of Euclid Data Products | `TBD_OVERVIEW_ID` | Shooby |
| 3. Python Firefly Data Access | `TBD_FIREFLY_ID` | Jaladh |
| 4. Accessing Euclid Data in the Cloud | `TBD_CLOUD_ID` | Troy |
| 6. Science Case: Euclid Galaxy Clusters | `TBD_CLUSTERS_ID` | Shooby |
| 7. Science Case: Euclid AGNs | `TBD_AGNS_ID` | Shooby |

Example — to publish the Firefly video:

```
# in docs/index.html, find:
src="https://www.youtube-nocookie.com/embed/TBD_FIREFLY_ID"
# replace with the real ID, e.g.:
src="https://www.youtube-nocookie.com/embed/abc123XYZ_0"
```

The Data Explorer section (2) already points at a public YouTube playlist and needs no swap. The Fornax section (5) plays a NASA-hosted MP4 directly — no YouTube ID involved.

## TBD checklist (clear before launch)

In `docs/index.html`:

- [x] Top intro paragraph
- [x] Header simplified — date/version and pointer links removed by design (per-section "Related resources" carry links)
- [ ] Section 1 intro + related resources + `TBD_OVERVIEW_ID`
- [x] Section 2 — intro and Euclid Data Explorer link done
- [ ] Section 3 — still needs `TBD_FIREFLY_ID` *(intro and Firefly GitHub link done)*
- [ ] Section 4 — still needs `TBD_CLOUD_ID` *(intro and IRSA cloud-access notebook link done)*
- [x] Section 5 — intro added; transcript and extra-resources lines removed (NASA Fornax link only)
- [ ] Section 6 — still needs `TBD_CLUSTERS_ID` *(intro, IRSA notebook link, and Bhargava+ 2025 reference paper done)*
- [ ] Section 7 — still needs `TBD_AGNS_ID` *(intro and AGN SOM notebook link done; notebook currently lives in `xoubish/Euclid_AGN_SOM` and will move into the `caltech-ipac/irsa-tutorials` repo after review — swap the link then)*
- [x] Footer contact email — Shoubaneh Hemmati &lt;shemmati@caltech.edu&gt;

Quick way to find what's left:

```
grep -n "TBD" docs/index.html
```

In this README:

- [x] Real published Pages URL captured (above)
- [ ] Confirm the link has been posted on euclid.caltech.edu

## Editorial conventions

- Every placeholder appears as both an HTML comment (`<!-- TBD: ... -->`) and a visible inline marker (`[TBD: ...]` wrapped in `<span class="tbd">`) so reviewers see the gap on the page and `grep TBD` finds them all.
- YouTube embeds use privacy-enhanced `youtube-nocookie.com`. Don't switch back to `youtube.com/embed/...` — the no-cookie domain avoids dropping tracking cookies on visitors who never click play.
- The Fornax MP4 is played via HTML5 `<video>` directly from `assets.science.nasa.gov`. Cross-origin video playback from github.io works without CORS config; no proxy needed.
- No analytics, no comments, no autoplay. Don't add any.

## Notes for collaborators

- Anything you put outside `/docs` (notes, drafts, planning docs, raw transcripts) stays private — go ahead and commit it here rather than juggling Drive links.
- If you want to preview a change before pushing to `main`, open `docs/index.html` in a browser locally. There is no staging environment.
