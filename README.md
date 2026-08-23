# ExplainerBoard

A shared whiteboard that runs entirely in the browser — no server. Drawing tools,
text, pan/zoom, undo/redo, SVG/PNG export, and **live peer-to-peer collaboration**
with cursors, all in one static `index.html`. Because there's no backend, it hosts
on GitHub Pages for free.

## Deploy to explainerboard.gcjana.in

1. Put `index.html` (and `CNAME`) in the repo that serves your Pages site.
   - If the site lives at the **root** of `gcjana.in`, this board probably belongs
     in a **subdirectory or its own repo** so it doesn't overwrite your homepage.
   - The included `CNAME` contains `explainerboard.gcjana.in`. Keep it **only** if
     this repo is the one mapped to that subdomain. If your existing repo already
     has a CNAME, don't add a second one — one CNAME per Pages site.
2. Commit and push.
3. In the repo's **Settings → Pages**, confirm the source branch/folder and the
   custom domain `explainerboard.gcjana.in`.
4. In your DNS (wherever gcjana.in is managed), add a **CNAME record**:
   `explainerboard` → `<your-github-username>.github.io`
5. Wait for DNS + Pages to issue HTTPS (a few minutes to an hour), then open
   https://www.explainerboard.gcjana.in

## Using it

- Pick a tool from the left dock (or press V P L R O T E). Colours and stroke
  width are in the bottom tray; **Fill** toggles filled shapes.
- **Scroll** to zoom, **hold Space + drag** (or drag empty space with the Select
  tool) to pan. The % chip resets the view.
- **Share** copies the room link. Anyone who opens that link joins the same board
  and you'll see each other's cursors live.
- **Board** menu: export SVG/PNG, save/open a `.json` board file, or clear.

## About "live" collaboration

Sync uses [Yjs](https://yjs.dev) over WebRTC (`y-webrtc`) through **public signaling
servers**. That's what makes zero-backend collaboration possible, but those servers
are community-run and can occasionally be down. When that happens the board simply
drops to **Solo** mode — it keeps working locally, you just won't sync with others.

For rock-solid collaboration you can later run your own tiny signaling server, or
swap the sync layer for Firebase/Supabase. Ask and I'll wire that in.

## Notes

- Boards are keyed by the `#room=…` id in the URL. No id = a fresh private room.
- Local drawings persist in your browser (IndexedDB) per room.
- Anyone with a room link can edit it — treat links like keys.
