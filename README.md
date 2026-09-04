# United MENA Playbook — website source

This folder is a ready-to-deploy copy of the site, reassembled from what was in the shared
"MENA Playbook" Claude project (the `index.html` and `chat.js` docs, plus the 24 uploaded images).
It's structured to drop straight into a new GitHub repo and deploy on Vercel with no path fixes.

## What's inside
- `index.html` — the full single-page site.
- `api/chat.js` — the serverless function behind the chat widget (Vercel convention: anything
  under `api/` becomes a serverless endpoint at the matching path, so this becomes `/api/chat`).
- `images/` — the 21 images `index.html` actually references, renamed to match exactly
  (e.g. the project's `ypomenamark.png` → `images/ypo-mena-mark.png`, `menamap.png` → `images/mena-map.png`).
- `images/_unused-extras/` — 3 files from the project that aren't referenced by this `index.html`
  (two duplicate map images, and `ypomenalogowhite.png`). Kept in case they're used elsewhere;
  safe to delete if not needed.

Note: `sarah.jpg` is ~6.2MB — much larger than the other headshots (5-17KB). Worth compressing
before or after the move; it will otherwise slow the page down for anyone loading it on mobile.

## Before you push this anywhere
Set `ANTHROPIC_API_KEY` as an environment variable in Vercel — do NOT hardcode it in `chat.js` or
commit it to the repo. When you stand up the new team-owned Vercel project, generate a **fresh**
API key for it rather than copying the old personal one over; then the old key can be revoked from
the manager's account without breaking anything new.

## The other thing this site depends on
`index.html` posts the access-gate signup and page-analytics beacon to a Google Apps Script Web
App URL (search the file for `script.google.com/macros/s/...`). That script writes to a Google
Sheet. This lives outside GitHub/Vercel entirely — check who owns that Apps Script + Sheet and
either share edit access with the team or move ownership, otherwise the manager stays a single
point of failure for signups and analytics even after the code itself is on a shared account.
