# ExplainerBoard

A shared whiteboard that runs entirely in the browser — no server. It mirrors most
of MIT CoCreate's toolset and hosts on GitHub Pages for free, because there's no
backend: drawing is client-side and collaboration is peer-to-peer.

## Features (vs CoCreate)

Tools: select/move, pan (H or hold Space), pen, line, rectangle, ellipse, text,
eraser. Marquee multi-select (drag empty space), shift-click to add/remove.

Styles: full colour palette + custom colour picker, four stroke widths, solid /
dashed / dotted lines, arrowheads (none / end / both), opacity slider, fill toggle.

Canvas: infinite pan & scroll-zoom, zoom in/out, reset to 100%, zoom-to-fit,
square **and** triangular grids, snap-to-grid, dark mode.

Pages: previous / next / add / duplicate, with a live page counter.

Editing: undo / redo, duplicate (Ctrl+D), copy/paste (Ctrl+C / Ctrl+V),
select-all (Ctrl+A), delete.

Collaboration: shareable room links, live labelled cursors, presence avatars,
head-count, editable name. Cursors hide when a peer is on another page.

Export & storage: export the current page as SVG or PNG, save/open the whole
multi-page board as a `.json` file, per-room offline persistence (IndexedDB).

### Not yet included (the three heavy ones)
- **LaTeX math** in text (CoCreate uses MathJax) — needs a math renderer like KaTeX.
- **Image embedding** — can be added as drag/drop & paste of image files.
- **Full time-travel history** — undo/redo covers the common case; a history
  scrubber is a larger build.
Each is a clean add-on — ask and I'll wire it in.

## Deploy to explainerboard.gcjana.in

1. Put `index.html` (and `CNAME`) in the repo that serves your Pages site. If
   `gcjana.in` itself is served from the same repo, put this in its own repo or a
   subfolder so it doesn't overwrite your homepage.
2. Keep the included `CNAME` (`explainerboard.gcjana.in`) only if this repo is the
   one mapped to that subdomain. One CNAME per Pages site.
3. Commit and push. In **Settings → Pages**, confirm the branch/folder and custom
   domain. In DNS, add a CNAME record: `explainerboard` → `<username>.github.io`.
4. Open https://explainerboard.gcjana.in once HTTPS is issued.

## Keyboard

V select · H pan · P pen · L line · R rect · O ellipse · T text · E eraser · G grid
Ctrl+Z undo · Ctrl+Shift+Z redo · Ctrl+C/V copy/paste · Ctrl+D duplicate · Ctrl+A all · Del delete

## About "live" collaboration

Sync uses Yjs over WebRTC (`y-webrtc`) through **public signaling servers** — that's
what makes zero-backend collaboration possible, but they're community-run and can
occasionally be down. When that happens the board drops to **Solo** and keeps
working locally. For always-on sync, run your own small signaling server or move the
sync layer to Firebase/Supabase. Anyone with a room link can edit — treat links like keys.
