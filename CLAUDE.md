# CLAUDE.md

whs_reborn: a static GitHub Pages site (custom domain in `CNAME`) that revives the old Windows Home Server 2007 promo material, recovered from Wayback Machine captures of microsoft.com. Flash (`.swf`) demos are played in the browser with the Ruffle emulator. Public repo; the content is archival, so treat the original media files as read-only.

## Layout
- `index.html` - home page: the "House Demo" player, a short note, and a link to `more.html`. `more.html` - the other salvaged items (video players, gallery, the book PDF).
- `*.swf`, `*.flv` at the repo root - recovered Flash movies and video (`Video-*.swf` wrap the matching `.flv`; `Microsoft-Home-Server-House.swf`, `hero_windowshomeserver.swf`, `ClearExternalPlaySeekMute.swf` are the player/skin pieces).
- `play/` - small per-video pages (`Video-Appliance`, `Video-File-Replication`, `Video-Photo-Backup`, `Video-Photo`) with their own `.flv`.
- `banners/` - banner images. `mommy-server-book.pdf` is hosted here directly instead of linking to archive.org.
- `.nojekyll`, `CNAME` - Pages config. Do not delete either.

## Run locally
- No build step, no package manager, no tests. Serve the folder (for example `python -m http.server 8000`) and open it in a browser. Pages use root-absolute paths such as `/Microsoft-Home-Server-House.swf`, so serve from the repo root.

## Gotchas
- Ruffle is loaded from unpkg in a `<script>` tag in each page, with its config set inline (`autoplay:"on"`, no splash). Pages need internet to load it. Check the script URL in the page before assuming a version.
- Every page ends with an inline script that sends a `navigator.sendBeacon` hit (path, referrer, and an approximate "City, Region, Country" looked up from the visitor's IP via get.geojs.io) to `papalanc.com/whs/hit`. Keep it in new pages for consistency, and flag it if a change would collect more than that.
- Large binary media is committed directly. Avoid re-committing or recompressing it without a reason.

## Deploy
- Push to `main`; the site is served by GitHub Pages. I did not find a workflow, tags or release process, so there are none to follow.
