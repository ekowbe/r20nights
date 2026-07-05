# R20 Nights — Handoff

_Updated: 2026-07-05_

## What this is
Static marketing site for **R20 Nights**, a Saturday-night student gathering at Columbia
(Columbia, NYU, CCNY, Pace). Two pages: `index.html` (landing) and `visit-us.html`.
Plain HTML/CSS — no build step, no framework.

## Current state
- Live at **r20.nyc**, auto-deploys on push to `main`. `vercel.json` enables clean URLs.
- Repo: `github.com/ekowbe/r20nights`.
- **Collaborator: Vania Senanu** — she owns `visit-us.html` and the Typeform/VisitorReach
  integration. Two open GitHub issues for her: #2 (favicon improvements) and #3 (redesign
  OG image to match dark/gold brand).

## Recent work (this session)
- Full content pass: Avery Hall removed everywhere, times corrected (6:30 doors / 7:00 PM),
  Pace University added to campus cards and RSVP form, Vision section updated to
  Found → Formed → Fielded.
- Frontend best-practices pass: mobile nav (hamburger now works — fullscreen overlay),
  skip link, focus rings, aria labels, non-blocking font loading, JSON-LD structured data.
- Connect section wired to `/visit-us` (Vania's Typeform page) — dummy form removed.
- `visit-us.html` redesigned: two-column layout, sticky header with time/location/promises.
- Voice audit: no "ministry", "the service", "the message", "our community" anywhere.
- git global user identity set to Ekow Bentsi-Enchill / ekow.bentsi.enchill@gmail.com.

## Open / pending
- [ ] Deep research report in progress (in-flight workflow): **should R20 add a statement
  of faith or central tenets section?** — awaiting results, discuss before implementing.
- [ ] Vania: OG image redesign (issue #3) — dark/gold, matches site aesthetic.
- [ ] Vania: Favicon + OG tag improvements (issue #2) — .ico, 180px touch icon,
  og:image:width/height, og:site_name.
- [ ] Campus card hangout details: all blocks are TBD — need real When/Where/Reach Out
  per hangout (Columbia ×5, NYU ×4, CCNY ×1, Pace ×1).
- [ ] Typeform colors: Vania needs to update in Typeform dashboard
  (bg #0a0a0a, text #f5f2ec, button #c9a84c / #0a0a0a).

## Key facts (do not change without checking)
- Saturday nights, 7:00 PM start, 6:30 PM doors. Location: Columbia University (no
  specific hall — not yet registered, keep low profile).
- Voice: peer ("we", "us"), never institutional. No "ministry", "the service", "the message".
- First Love Church: footer only, never subject of a sentence.
- Three campuses + Pace: Columbia (5 hangouts), NYU (4), CCNY (1), Pace (1).

## Key commands
```bash
cd ~/Projects/r20nights
open index.html            # local preview — just open in browser, no server needed
git push origin main       # deploys to Vercel automatically
```

## Gotchas
- No build step. Edit HTML/CSS directly, open in browser to test, push to deploy.
- `.claude/launch.json` exists locally for preview server — not committed, that's fine.
- R20 ministry docs (leadership guide, meeting notes) stay on Desktop, not in this repo.
