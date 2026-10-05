# Vaud Newcomer Admin Kit (static site)

Plain HTML + one CSS file (`style.css`). No JavaScript, no build step needed to view,
no external fonts, CDNs, analytics, cookies or embeds. All internal links are relative,
so the site works at a domain root or under a `/repo-name/` subpath.

View locally: open `index.html` in a browser, or run `python3 -m http.server` in this folder.

## Deploy to GitHub Pages (later)

Option A: site at the repository root
1. Create a repository and push the **contents of this folder** (including the empty
   `.nojekyll` file) to the `main` branch root.
2. In the repo: Settings -> Pages -> Build and deployment -> Source: "Deploy from a branch",
   Branch: `main`, folder: `/ (root)`. Save.
3. The site appears at `https://<user>.github.io/<repo-name>/`.

Option B: keep the build script in the repo and serve from `/docs`
1. Put `build.py`, `templates/`, `content/` and the source markdown files in the repo,
   and generate into `docs/`: `python3 build.py --out docs`.
2. Commit `docs/` (with `.nojekyll`), then Settings -> Pages -> Branch: `main`, folder: `/docs`.

`.nojekyll` tells GitHub Pages to serve the files as-is (no Jekyll processing).

## Updating content

The pages are generated from markdown by `build.py` (Python standard library only), which
lives one folder up (`/workspace/vaud-newcomer-kit/build.py` on the box). The generated HTML is
kept here, so the site works without running anything.

- Sources: `vaud-newcomer-admin-kit.md` (permit, transport, bank, phone, Serafe, driving licence),
  `student-tax-avs-lamal.md` (tax, AVS, LAMal), `epfl-sections.md` + `epfl-sources.md` (EPFL).
- Pages are ordered by arrival stage (Before you arrive / First 2 weeks / First month / Later):
  `GROUPS` and `PAGES` in `build.py`. That order drives the nav, the home cards and previous/next links.
- "Related" blocks: `RELATED` in `build.py`. Home "Start here" checklist: `content/start-here.md`.
- Timeline entries: `TIMELINE` in `build.py`. Each must quote its source verbatim (the build stops
  if a quote is not found), so only explicitly stated deadlines appear.
- "Past" badges on the timeline are computed from the system date **at build time**.
  Re-run `python3 build.py` to refresh them; the committed HTML reflects the last build date.
- Items the sources mark "To verify" keep a visible red "To verify" badge.
- New topics can start as placeholder pages ("Content coming soon"): add a `PAGES` entry with
  `source=None`, then fill it by writing `content/<slug>.md` and re-running `python3 build.py`.

Disclaimer: orientation guide only, not official, legal, tax or insurance advice. Always check
the linked official sources.

## Also in this folder (5 Oct 2026)

- `fr/`: French versions of Home, the printable checklist, Permit & commune, LAMal and EPFL housing
  (language switch EN ↔ FR on those pages; untranslated topics link back to the English page).
- `glossary.html`: plain-language glossary, linked from every page's nav and footer.
- `sitemap.xml` / `robots.txt`: path-only sitemap entries because no public URL is approved yet. At go-live,
  rebuild with `python3 build.py --base-url https://<user>.github.io/<repo>` so the `<loc>`s and the
  `Sitemap:` line become absolute.
