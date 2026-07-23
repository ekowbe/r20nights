# R20 Nights — Handoff

_Updated: 2026-07-19_

## What this is
Static marketing site for **R20 Nights**, a Saturday-night student gathering at Columbia
(Columbia, NYU, CCNY, Pace). Three pages: `index.html` (landing), `visit-us.html` (orphaned —
redirect in place, file still on disk), `leadership.html`. Plain HTML/CSS — no build step, no framework.

## Current state
- Live at **r20.nyc**, auto-deploys on push to `main`. `vercel.json` enables clean URLs + `/visit-us` redirect.
- Repo: `github.com/ekowbe/r20nights`.
- **Collaborator: Vania Senanu** — one open GitHub issue: #2 (favicon improvements). Issue #3 (OG image) is done this session.

## Recent work (2026-07-19) — moving muted photo grid (hero)
- **Deep research done (104-agent verified run): Conditional GO.** Motion heroes show NO proven
  conversion upside (Unbounce ~35k-page study: neutral-to-negative; click-through pages like ours
  did worse with video), BUT real photos of the actual crowd strongly beat stock/no-imagery for
  skeptical Gen-Z (NN/g eye-tracking + real-vs-stock conversion evidence). Verdict: the PHOTOS are
  the value, the MOTION is optional garnish — ship static-first, motion as A/B enhancement.
- **Spec (research-backed):** hero-only (not full page); CSS-transform-only drift (~75-95s loops,
  compositor-safe, no JS); 12-18 tiles ≤30KB each, total ≤450KB; photos desaturated + dimmed;
  #0a0a0a scrim heavy at center so text clears WCAG 4.5:1 vs worst-case (brightest) tile;
  `prefers-reduced-motion` → static collage.
- **TWO variants built & browser-verified (desktop + mobile), both local, NOT committed/pushed:**
  - `motion-demo.html` — **grid variant**: 3 rows of tiles drifting diagonally behind the existing
    LEFT-ALIGNED hero (matches nephew's webflow reference). Pure CSS.
  - `motion-demo-film.html` — **film-strip variant**: single 35mm strip (sprocket rails, gold
    edge-printing "R20 NIGHTS/SATURDAY/COLUMBIA", frame numbers, warm sepia grade, grain, vignette,
    subtle gate-weave) scrolling behind a CENTERED title-card. Adapted from Ekow's `vhs-title-goldtape.html`
    ("Midnight Rewind") reference — but STRIPPED the VHS-arcade layer (magenta/cyan RGB glitch,
    REC/timecode HUD, "Press play") which read as cheesy for the skeptical-student persona. Kept the
    film-strip skeleton + warm grade, re-skinned to R20 gold/Playfair. This is the stronger of the two.
  - Both use the same 17 tiles in `img/nights/` (320KB total). Serve via `.claude/launch.json` (note:
    preview tool rewrote the dir — symlink `~/Desktop/r20nights` → project exists as workaround).
- **Photo selection:** 74 pics reviewed from `~/Downloads/R20 Docs/R20 pics/`. 17 picked for
  campus identity (Low Library night, Columbia lawn, subway, Edge skyline), warmth (banquet,
  restaurant, beach), and moody pro shots (Gospel Encounter/Founders Day — watermarks cropped).
- [ ] **CONSENT GATE (blocking before deploy):** every identifiable face needs affirmative consent
  before shipping publicly (church-liability best practice; a religious-gathering photo also reveals
  religious affiliation). Any minors → exclude or make unidentifiable. Run this pass over the 17.
- [ ] Decide static-first vs motion; then integrate into `index.html` hero and deploy.

## Recent work (2026-07-19/20) — DECISIONS: film strip + photo strategy + /hangouts
- **Film-strip variant CHOSEN** (`motion-demo-film.html`) over the grid. Grid speed was too slow to
  read as motion — bumped rows to 44s/38s (~43px/s) so it's clearly ambient-but-moving.
- **Photos re-categorized by Ekow** in `~/Downloads/R20 Docs/R20 pics/`: `Bible Hangouts/` (7 candid
  dorm-lounge selfies), `Misc Gatherings/` (9 larger candid group/campus/transit), `Professional Pics/`
  (9 event-photog "Gospel Encounter/Founders Day" — watermarked).
- **CONSENT: Ekow confirms he HAS their okay** for these subjects. (Consent gate on the OLD 17-tile set
  is superseded; use the newly-categorized set.)
- **Watermarks CROPPED** — all 9 Professional pics → `Professional Pics/cropped/*_crop.jpg` (bottom
  15% landscape / 10% portrait removes the bottom-right watermark; faces are upper/center, untouched).
  Non-destructive (originals kept).
- **2nd deep-research run (108-agent verified) — photo-type strategy, key confirmed findings:**
  - Anti-polish thesis holds: over-polished imagery triggers "being sold to" distrust in Gen Z;
    candid/lo-fi = "from a friend." BUT genuinely low-quality also hurts ("can't afford better").
    → **authentic beats polished, competent-authentic beats sloppy.**
  - Raised-hands worship "reads as weird even to insiders" → keep overt-worship imagery MINIMAL.
  - **Lifeway (primary, 3-0): only 35% of unchurched attend a WORSHIP SERVICE when invited vs 62% a
    COMMUNITY/SMALL-GROUP MEETING** → the Bible Hangout is ~2× more attendable; it's the lowest-barrier
    front door for a skeptic, not a secondary extra.
  - 9-in-10 Gen Z report social anxiety in group settings; visit-preview pages that SHOW the actual
    room + describe the flow reduce first-visit anxiety (churchtrac, guppyfish 3-0).
  - Text-over-image: keep 4.5:1 contrast + scrim; busy/faded bg hurts legibility (NN/g, Smashing).
  - Research output: `~/.claude/.../tasks/wyuurxmcj.output` (synthesis field stubbed; verified
    claims + sources intact in the journal).
- **PHOTO MIX DECIDED:** film strip = mostly Misc Gatherings + Bible Hangouts (candid/peer), 1–2
  cropped Professional for range/competence, worship shots minimal. `/hangouts` gallery = pure candid
  Bible Hangouts.
- **DECISION — `/hangouts` page:** APPROVED. Primary hero CTA stays `join.r20.nyc/welcome`. Link
  placement DECIDED = **secondary hero link** ("See what a hangout's actually like →") directly under
  the main CTA — the low-commitment peek door for the not-ready-for-Saturday skeptic.
- **PHOTO SPLIT REFINED (Ekow's call, I agreed + pushed back once):** Professional → FILM STRIP;
  Bible Hangouts → /hangouts page. Rationale: the film grade (dim/warm/grain/small/moving) erases
  polish signals, and pro shots (high-contrast, single emotive face) survive shrinking best; candids
  do their real anti-anxiety work on the /hangouts page where authenticity is judged. Pushback taken:
  don't make strip 100% pro → interspersed ~4 candid Misc so it reads community, not lookbook.

### BUILT THIS SESSION (local, NOT committed/pushed yet)
- **Photo processing (non-destructive):**
  - `img/film/f01..f13.jpg` — 9 cropped Professional + 4 candid Misc interspersed (900px, q52, ~1.0MB total, lazy-loaded).
  - `img/hangouts/h01..h11.jpg` — 7 Bible Hangouts + 4 supporting Misc (1400px, q72, ~3.6MB — FINE for a
    below-fold gallery but could compress later).
- **`motion-demo-film.html`** — updated to use `img/film/`. Browser-verified desktop: pro frames survive
  the warm/dim treatment with clear focal faces, candids break the rhythm. Reads cinematic + real.
- **`hangouts.html`** — NEW `/hangouts` page, built native to site (same tokens/nav/footer). Structure:
  hero "What a hangout's *actually like*" → 4 flow-fact cards (Who ~10 students / When midweek / Where
  dorm lounge / What talk it out) → honest peer-voice blurb ("You don't have to believe anything to show
  up" pull-quote) → masonry candid gallery (11 imgs, a few anxiety-lowering captions) → CTA
  (`?src=r20nyc-hangouts-cta`) → footer. Verified: all 11 imgs 200 OK, layout contiguous, hero+facts
  render clean. (Preview-pane scroll desyncs on in-frame #anchor jumps → black screenshots mid-gallery;
  it's a pane artifact, page is fine.)

- **⚠️ STICKY CHURCH CORRECTION (Ekow caught this — supersedes the "secondary hero link" decision):**
  Per `~/Downloads/R20 Docs/.../Sticky_Church_Deep_Dive_Notes.md` Ch 18 (the Cho analysis) — and R20's
  OWN locked architecture — **a dorm/home Bible study is MORE threatening than the public gathering for a
  cold secular skeptic** ("intense, maybe cultish, can I leave?"). So the GATHERING is the low-threat cold
  front door; the HANGOUT is entered via belonging/relationship, NEVER cold. My earlier "hangout = the
  easiest first yes" framing was the exact Cho mistake. (My Lifeway "62% community meeting" stat was about
  broad social events, not intimate home studies; and my own "9-in-10 Gen Z social anxiety" finding actually
  supports Osborne — the intimate room is higher-anxiety than the anonymous gathering.)
  - **FIXED `hangouts.html` copy:** hero now "Saturday night is the easy place to start. This is what comes
    next…"; closing CTA now "Start with Saturday → Come to R20 Nights" (routes cold visitors to the gathering).
    The page's JOB is now demystification/transparency (counters the "cultish" fear by showing the room), NOT
    cold-front-door recruiting.
  - **/hangouts LINK PLACEMENT DECIDED (data/practitioner-driven):** put in the EXISTING `#campuses` section
    ("Bible Hangouts on your campus"), NOT the hero. Added `<a class="hangout-peek" href="/hangouts">See what
    a hangout's actually like →</a>` under the section subtitle + `.hangout-peek` CSS. DOM-verified present,
    gold, inside #campuses. Rationale: hero pushes ONE front door (gathering); transparency link sits mid-page
    exactly where the visitor is already asking "what are these hangouts?"; satisfies Sticky Church + the
    churchtrac/guppyfish "show the actual space" anxiety-reduction finding.
  - Local note: `/hangouts` clean URL 404s on the simple preview server but works in prod (vercel cleanUrls:true, confirmed).

### ✅ FILM STRIP INTEGRATED INTO index.html (this session, local, NOT pushed)
- Film strip is now the **hero background** of the real `index.html` (kept the existing left-aligned hero
  content — title/subtitle/CTAs/detail all intact; strip sits behind at z-index 0, text at z-index 1).
- Markup: `.hf-zone > .hf-tape > .hf-strip#heroStrip` + `.hf-scrim`, inserted after `.hero-lines`. CSS is
  `hf-`-prefixed (no collisions). JS builds 13 frames ×2 from `img/film/f01..f13.jpg` (added into the
  existing hero `<script>`; first 3 eager, rest lazy).
- **Scrim = left-weighted on desktop** (dark left for the headline, photos peek right); **vertical +
  slight left-fade on mobile** (lightened middle band 0.6 so the muted pics actually show — first pass
  was too dark and hid the strip). Browser-verified desktop + mobile (375px): headline crisp, photos
  visible, no console errors, all `img/film` 200 OK. Respects `prefers-reduced-motion`.
- Photo sets rebuilt after Ekow re-curated: `img/hangouts/h01..h11` = 7 current Bible Hangouts + 4 misc
  (BH set changed — non-hangout shots swapped out; h07 has an actual "BIBLE HANGOUT" sign). Snacks caption
  moved to h02 (shows food, per research).

- **RESEARCH LANDED (photo types):** 110 adversarially-verified claims (journal recovered; synth step
  failed but claims intact). Verdict CONFIRMS the split — Professional leads the strip (high-contrast
  single-face survives dim/small/moving; busy candids "turn to mud"), candids do authenticity work on
  /hangouts. Overt worship imagery REPELS cold skeptics (keep near-zero — guitar shot is the ceiling).
  Predominantly-Black imagery is an ASSET (2025 J. Marketing meta-analysis: coethnic draws minority
  self-ID, no majority backlash) — just avoid "homogenization" (show variety). Averted-gaze candids beat
  direct-eye-contact for belonging. Full rubric delivered in chat.

### ✅ AUDIENCE TRIAGE PASS (this session — audited whole site vs "Marcus" the skeptic)
- **Footer** "Community → Bible Hangouts" repointed `#campuses` → `/hangouts`. (Decided NOT to add /hangouts
  to top nav/mobile menu — that would over-promote the hangout as a cold front door = the Cho mistake;
  "Campuses" nav already routes to the #campuses section that holds the in-section /hangouts link.)
- **Softened "What We Believe" → "Where We're Coming From"** (Ekow's final wording): dropped the creedal
  enumeration (life/death/resurrection) + Bible-authority line; honest but disarming. "…there's room for you in R20."
- **Vision reframed visitor-facing:** title "What we're building"→"Where this goes"; KILLED "Hearts on fire
  for New York"; lead →"…start saving a seat for the next person"; 3rd card "Fielded (leaders raise leaders,
  new communities across the city)" → "Welcoming (the person who felt like an outsider becomes the one making
  room for someone else)." Removed insider/church-planting tone.
- **Merch:** removed the advertised "free R20 merch just for showing up" Connect promise (still given in
  person, not dangled). Connect promises now 3 clean ones.
- All browser-verified live. Site's anxiety-reduction spine (No Awkward Moments / First time is the hardest
  part / Doubt doesn't disqualify you) left intact — it's the strongest Marcus-facing asset.

- **STILL TODO (next) — Ekow owns #1-2:**
  1. Campus cards all "TBD" (When/Where/Reach-out, dead href="#") — FILL or hide before launch (Ekow: "fixed soon").
  2. 10DLC / Oikos SMS must be live before the "a real person will text you" promise goes out (Ekow: "fixed soon").
  3. Wire nav/footer/mobile links if any remain; compress `img/hangouts/` (~3.3MB) before deploy.
  4. Then commit + push (auto-deploys to Vercel). NOTHING committed/pushed yet — live r20.nyc untouched.
  2. Add `/hangouts` clean-URL handling (vercel cleanUrls already on → `hangouts.html` serves at `/hangouts`; verify).
  3. Wire nav/footer links to `/hangouts` on index + leadership.
  4. Consider compressing `img/hangouts/` (~3.6MB) before deploy.
  5. `?src=` audit; reduced-motion fallback already in film demo.
  6. Then commit + push (auto-deploys to Vercel).

## Recent work (2026-07-18) — continued
- **Design direction held — dark/gold/Playfair identity stays.** Adelaide (social media) proposed a white/blue/Poppins redesign ("Apple-meets-church-plant"). Scored against 5 criteria (differentiation, audience alignment, tonal fit, rebrand cost, longevity): current design 23/25, proposed 8/25. Decision: keep current identity, make 3 targeted improvements. Decision brief shared with Adelaide as a public artifact. **A/B comparison tool** built (artifact https://claude.ai/code/artifact/07c1b422-079c-4cbd-83c3-d9f9980507b9) — tracks votes + comments in localStorage, pass-the-phone flow for hallway research with students. Run this if you want actual audience data before closing the question.
- **3 targeted improvements identified (not yet implemented):**
  1. Body text: bump DM Sans from weight 300 → 400 for mobile legibility (one CSS line)
  2. Section padding: audit and increase vertical gap between sections at 375px breakpoints
  3. Muted interactive text: raise opacity from ~50% → 65% on hover/interactive states

## Recent work (2026-07-18) — earlier
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
