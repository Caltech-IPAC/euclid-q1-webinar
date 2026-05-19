# Euclid Q1 Webinar Series

Landing page for the ENSCI/IPAC webinar series walking through Euclid's Q1 data release.

This repo is **private**. Only the `/docs` folder is published to GitHub Pages — everything outside `/docs` (this README, internal notes, drafts) stays private to the repo.

## Where the live site lives

- **Source**: `docs/index.html` (+ `docs/styles.css`) on the `main` branch
- **Published URL**: `https://<org-or-user>.github.io/Euclid-q1-webinar/` *(fill in once Pages is enabled)*
- **Linked from**: [euclid.caltech.edu](https://euclid.caltech.edu/) — the published URL above gets posted there once we're ready to launch.

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

- [ ] Top intro paragraph
- [ ] Webinar release date / version note
- [ ] Euclid Q1 documentation link (header)
- [ ] IRSA Euclid pages link (header)
- [ ] Section 1 intro + related resources + `TBD_OVERVIEW_ID`
- [ ] Section 2 intro + Data Explorer docs link
- [ ] Section 3 intro + related resources + `TBD_FIREFLY_ID`
- [ ] Section 4 intro + related resources + `TBD_CLOUD_ID`
- [ ] Section 5 intro + transcript + extra Fornax resources
- [ ] Section 6 intro + related resources + `TBD_CLUSTERS_ID`
- [ ] Section 7 intro + related resources + `TBD_AGNS_ID`
- [x] Footer contact email — Shoubaneh Hemmati &lt;shemmati@caltech.edu&gt;

Quick way to find what's left:

```
grep -n "TBD" docs/index.html
```

In this README:

- [ ] Real published Pages URL (replace `<org-or-user>` above)
- [ ] Confirm the link has been posted on euclid.caltech.edu

## Editorial conventions

- Every placeholder appears as both an HTML comment (`<!-- TBD: ... -->`) and a visible inline marker (`[TBD: ...]` wrapped in `<span class="tbd">`) so reviewers see the gap on the page and `grep TBD` finds them all.
- YouTube embeds use privacy-enhanced `youtube-nocookie.com`. Don't switch back to `youtube.com/embed/...` — the no-cookie domain avoids dropping tracking cookies on visitors who never click play.
- The Fornax MP4 is played via HTML5 `<video>` directly from `assets.science.nasa.gov`. Cross-origin video playback from github.io works without CORS config; no proxy needed.
- No analytics, no comments, no autoplay. Don't add any.

## Notes for collaborators

- Anything you put outside `/docs` (notes, drafts, planning docs, raw transcripts) stays private — go ahead and commit it here rather than juggling Drive links.
- If you want to preview a change before pushing to `main`, open `docs/index.html` in a browser locally. There is no staging environment.
