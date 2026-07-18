# R20 Nights — Handoff

_Updated: 2026-07-18_

## What this is
Static marketing site for **R20 Nights**, a Saturday-night student gathering at Columbia
(Columbia, NYU, CCNY, Pace). Three pages: `index.html` (landing), `visit-us.html` (orphaned —
redirect in place, file still on disk), `leadership.html`. Plain HTML/CSS — no build step, no framework.

## Current state
- Live at **r20.nyc**, auto-deploys on push to `main`. `vercel.json` enables clean URLs + `/visit-us` redirect.
- Repo: `github.com/ekowbe/r20nights`.
- **Collaborator: Vania Senanu** — one open GitHub issue: #2 (favicon improvements). Issue #3 (OG image) is done this session.

## Recent work (2026-07-18)
- **OG image redesigned** — new dark/gold 1200×630 card deployed to `favicon/openGraphTag-favicon.png`.
  Dark `#0a0a0a` background, R20 wordmark (R cream / 20 gold), Playfair Display 900, eyebrow
  "SATURDAY NIGHTS · NEW YORK", Playfair italic tagline, school names muted at bottom. Closes
  Vania's issue #3. **OG tagline is in active discussion** — current: "A space for the questions
  everyone's afraid to ask." Direction: curiosity-generating, naming a question Marcus already
  carries (e.g. a fall talk title). Not yet resolved — do not deploy a new tagline without deciding.
- **All CTAs rewired `/hi` → `/welcome`** across `index.html` + `visit-us.html`. Rule: the
  website always links to **`join.r20.nyc/welcome`** (cold/discovery door); only the physical
  at-a-Night QR/NFC card uses `/hi`.
- **Mobile nav** CTA: "Join Us Saturdays" → "Come to R20 Nights".
- **Connect section** CTA: "I'm Coming →" → "I want to come →".
- **First Love Church footer column** removed from `index.html` — First Love stays in the footer
  brand blurb only, never a nav column header.
- **`vercel.json`**: `/visit-us` 302-redirects → `join.r20.nyc/welcome?src=r20nyc-visit`. File
  `visit-us.html` is orphaned (no internal links point to it) but kept on disk for now.
- **Homepage footer** carries legal name **"R20 Campus Ministry"** + address
  (112-25 Queens Blvd, NY 11375) for Twilio 10DLC flag 18601.
- `.claude/` gitignored.

## Recent work (2026-07-16)
- **What We Believe** paragraph added inside the "Who We Are" section (`index.html`).
- **`leadership.html`** (new page) — `/leadership`. Bishop James Quist-Therson + Pastor Ekow
  Bentsi-Enchill, exact titles, tie line, 112-25 Queens Blvd NY 11375, ekow@r20.nyc. Built
  for Twilio 10DLC compliance.
- **`visit-us.html`** — Typeform removed entirely. Right column has two Oikos CTAs.
  Left column copy still stale (see open items below).

## Open / pending
- [ ] **OG image tagline** — current placeholder is stale. Direction: curiosity-generating,
  naming a question Marcus already carries. Candidates: fall talk titles ("Is There Actually
  a God?", "Your Worth Is Not Your GPA", "Why Does Injustice Still Bother You?"). Decide,
  then rebuild OG image from `og-image.html` in the scratchpad and redeploy.
- [ ] **`visit-us.html` left column copy** — subheader still says "Fill out the form and one
  of us will be in touch before you show up." Rewrite to describe what Saturday nights are;
  right column handles the CTA. OR delete the file entirely — redirect already in place.
- [ ] **`visit-us.html` OG/meta description** — still says "Let us know you're coming."
  Update to match current voice if the page stays.
- [ ] **Twilio DNS verification** — Add TXT record to r20.nyc on Namecheap:
  - Host: `twilio` · Type: TXT
  - Value: `twilio-domain-verification=988297391b5b1ba03b8cb1588fffdcf5`
  - Then hit "Check verification" in Twilio console.
- [ ] **`leadership.html` photos** — initials placeholders (JQ / EB) live. Swap in real photos.
- [ ] **`leadership.html` bios** — Ekow to approve/refine both before treating as final.
- [ ] **First Love New York public link** — needed for Twilio reply as second public source
  for the address. Add to leadership page once confirmed.
- [ ] Vania: Favicon improvements (issue #2).
- [ ] Campus card hangout details: all blocks TBD — need real When/Where/Reach Out
  per hangout (Columbia ×5, NYU ×4, CCNY ×1, Pace ×1).
- [ ] **The talk copy** — "What to Expect" currently says "built around the questions students
  actually carry." Recommend naming specific questions (2–3 from the fall arc titles) so Marcus
  has a concrete intellectual hook before he shows up.

## Oikos CTA map (`?src=` values)
| Placement | Label | src tag |
|---|---|---|
| Hero | New here? Come to R20 Nights | `r20nyc-home` |
| Nav / Mobile nav | Come to R20 Nights | `r20nyc-nav` |
| Times section | Come to R20 Nights | `r20nyc-times` |
| Connect section | I want to come → | `r20nyc-connect` |
| Footer | Come to R20 Nights | `r20nyc-footer` |
| visit-us primary (redirect) | — | `r20nyc-visit` |
| visit-us secondary (ask) | Ask us anything | `r20nyc-ask&ask=1` |

## Key facts (do not change without checking)
- Saturday nights, 7:00 PM start, 6:30 PM doors. Location: Columbia University (no
  specific hall — not yet registered, keep low profile).
- Voice: peer ("we", "us"), never institutional. No "ministry", "the service", "the message".
- First Love Church: footer brand blurb only, never a nav column or subject of a sentence.
- Three campuses + Pace: Columbia (5 hangouts), NYU (4), CCNY (1), Pace (1).
- R20 Campus Ministry address: 112-25 Queens Blvd, New York, NY 11375.
- Contact: ekow@r20.nyc.
- **All site CTAs → `join.r20.nyc/welcome`** (cold/discovery). At-a-Night QR/NFC card → `/hi`.

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
- OG image source lives at the scratchpad `og-image.html` (served via local Python server at
  8743; Chrome headless screenshots it). If rebuilding: `python3 -m http.server 8743` from
  the scratchpad dir, then Chrome headless `--window-size=1200,630`.
- R20 ministry docs (leadership guide, meeting notes) stay on Desktop, not in this repo.
