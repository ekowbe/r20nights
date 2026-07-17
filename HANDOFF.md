# R20 Nights — Handoff

_Updated: 2026-07-16_

## What this is
Static marketing site for **R20 Nights**, a Saturday-night student gathering at Columbia
(Columbia, NYU, CCNY, Pace). Three pages: `index.html` (landing), `visit-us.html`, and
`leadership.html`. Plain HTML/CSS — no build step, no framework.

## Current state
- Live at **r20.nyc**, auto-deploys on push to `main`. `vercel.json` enables clean URLs.
- Repo: `github.com/ekowbe/r20nights`.
- **Collaborator: Vania Senanu** — two open GitHub issues for her: #2 (favicon improvements)
  and #3 (redesign OG image to match dark/gold brand).

## Recent work (2026-07-16, cont. — Oikos chat)
- **All CTAs rewired `/hi` → `/welcome`** (the Oikos cold/discovery door) across `index.html`
  + `visit-us.html`. Rule: the website links to **`join.r20.nyc/welcome`** (site visitors
  haven't been to a Night); only the physical at-a-Night QR card uses `/hi`.
- **`vercel.json`**: `/visit-us` now 302-redirects → `join.r20.nyc/welcome?src=r20nyc-visit`.
- **Homepage footer** now carries the legal name **"R20 Campus Ministry"** + address
  (112-25 Queens Blvd, NY 11375) — for **Twilio 10DLC flag 18601** (business-name ↔ website).
- `.claude/` now gitignored.
- **`visit-us.html` removed** — its reassurance context already lives on the homepage
  (`#times` "Come as you are" + `#connect` "First time is the hardest part" promise list),
  so no separate page needed. The `/visit-us` → `/welcome` redirect stays as a legacy
  fallback so any old link still forwards to the capture.

## Recent work (this session)
- **What We Believe** paragraph added inside the "Who We Are" section (`index.html`), as a
  full-width second row in the `.what-grid`, separated by a gold divider. Copy finalized:
  *"We're a gathering of students who take Jesus seriously — his life, his death, his
  resurrection, and what he asks of us now. The Bible shapes how we read the world, and we'd
  rather work it out together than alone. Whatever you're making of any of it, there's room
  for you here. You don't need to have it figured out to show up on a Saturday night."*
- **`leadership.html`** (new page) — `/leadership`. Bishop James Quist-Therson + Pastor Ekow
  Bentsi-Enchill, exact titles, tie line, 112-25 Queens Blvd NY 11375, ekow@r20.nyc. Built
  for Twilio 10DLC compliance (public source linking Ekow to R20 Campus Ministry).
- **`visit-us.html`** — Typeform removed entirely. Right column now has two Oikos CTAs:
  primary "Come to R20 Nights" → `join.r20.nyc/hi?src=r20nyc-visit`, secondary "Ask us
  anything" → `join.r20.nyc/hi?src=r20nyc-ask&ask=1`. Left column copy needs rewrite
  (currently still references "Fill out the form" — stale from Typeform era).
- **`index.html`** — All CTAs now route straight to Oikos (no intermediate /visit-us):
  hero, nav, mobile nav, times section, connect section, footer. Each has a unique `?src=`
  tag for analytics. "Plan a Visit" removed from footer per spec.

## Open / pending
- [ ] **Twilio DNS verification** — Add TXT record to r20.nyc on Namecheap:
  - Host: `twilio` · Type: TXT
  - Value: `twilio-domain-verification=988297391b5b1ba03b8cb1588fffdcf5`
  - Then hit "Check verification" in Twilio console.
- [ ] **`leadership.html` photos** — initials placeholders (JQ / EB) are live. Swap in
  real photos when ready.
- [ ] **`leadership.html` bios** — Ekow to approve/refine both bios before treating as final.
- [ ] **First Love New York public link** — needed for Twilio reply as second public source
  for the address. Add to leadership page once confirmed.
- [ ] Vania: OG image redesign (issue #3) — dark/gold, matches site aesthetic.
- [ ] Vania: Favicon + OG tag improvements (issue #2).
- [ ] Campus card hangout details: all blocks are TBD — need real When/Where/Reach Out
  per hangout (Columbia ×5, NYU ×4, CCNY ×1, Pace ×1).
- [ ] Typeform colors: Vania — may no longer be needed now that Typeform is removed from
  visit-us. Confirm with Vania whether Typeform is still used anywhere.

## Oikos CTA map (`?src=` values)
| Placement | Label | src tag |
|---|---|---|
| Hero | New here? Come to R20 Nights | `r20nyc-home` |
| Nav / Mobile nav | Come to R20 Nights | `r20nyc-nav` |
| Times section | Come to R20 Nights | `r20nyc-times` |
| Connect section | I'm Coming → | `r20nyc-connect` |
| Footer | Come to R20 Nights | `r20nyc-footer` |
| visit-us primary | Come to R20 Nights | `r20nyc-visit` |
| visit-us secondary (ask) | Ask us anything | `r20nyc-ask&ask=1` |

## Key facts (do not change without checking)
- Saturday nights, 7:00 PM start, 6:30 PM doors. Location: Columbia University (no
  specific hall — not yet registered, keep low profile).
- Voice: peer ("we", "us"), never institutional. No "ministry", "the service", "the message".
- First Love Church: footer only, never subject of a sentence.
- Three campuses + Pace: Columbia (5 hangouts), NYU (4), CCNY (1), Pace (1).
- R20 Campus Ministry address: 112-25 Queens Blvd, New York, NY 11375.
- Contact: ekow@r20.nyc.

## Key commands
```bash
cd ~/Projects/r20nights
open index.html            # local preview — just open in browser, no server needed
git push origin main       # deploys to Vercel automatically
```

## Gotchas
- No build step. Edit HTML/CSS directly, open in browser to test, push to deploy.
- `.claude/launch.json` exists locally for preview server — not committed, that's fine.
- All inbound CTAs must keep `?src=` tags — they drive Oikos/Reach analytics.
- Do NOT build a form on r20.nyc — all site capture goes through `join.r20.nyc/welcome`
  (Oikos cold door); the at-a-Night QR card uses `/hi`. Keep `?src=` tags on every link.
- R20 ministry docs (leadership guide, meeting notes) stay on Desktop, not in this repo.
