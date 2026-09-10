# `/neighborhoods` and `/neighborhoods/*` — structure + literal copy

## THE RULE FOR THESE PAGES
Every **number** on these pages comes from a live widget — never from written copy. Do not write
median prices, school ratings, population figures, commute times, days-on-market or "best of"
claims into prose. If a widget cannot supply a figure, omit the figure. Never estimate one.

Written copy on these pages is limited to genuine local knowledge supplied by Team Sid.
Where it is marked **[LOCAL — TEAM SID]** it must be supplied or approved by Heather or Jeremy
before the page is built. Do not generate it.

---

# `/neighborhoods` — hub page

**H1:** `Tampa Bay Neighborhoods`
**Sub:** `We've lived here our whole lives. Here's what we know about the places we serve.`

**Body:**
> Every neighborhood in Tampa Bay has its own character — how quickly homes move, what you get for
> your money, who tends to move there and why. These pages are where we share what we know, with
> live listing data alongside it.

**Widget:** Community Areas Widget — listing count + image per area, linking to each area page.

**Areas, in this order:** Lutz · Land O' Lakes · Wesley Chapel · Northdale · North Tampa

**Closing CTA:** `Not sure which area fits? Let's talk.` → `/contact`

---

# `/neighborhoods/<area>` — template, applied to all five

Structure, top to bottom:

1. **H1:** `Homes for Sale in <Area>, FL`
2. **Intro** — **[LOCAL — TEAM SID]** 2–3 sentences of genuine local knowledge. See drafting
   prompt below.
3. **Widget:** Community Listings Stats *(most popular / most and least expensive)*
4. **Widget:** Dream Neighborhood *(maps, schools, demographics, commute, points of interest)*
5. **Widget:** Census Bureau Data
6. **Widget:** Google Map Widget scoped to the area's saved link
7. **H2:** `Current Listings in <Area>` → live listings via the area's IDX saved link
8. **Closing block** — literal, identical on every area page:
   **H2:** `Thinking About <Area>?`
   > We can tell you what's actually moving here, what it's going for, and whether it fits what
   > you're looking for. No pressure either way.
   **CTAs:** `See All <Area> Homes` → the area's IDX saved link ·
   `Ask Us About <Area>` → `/contact`

## Saved-link bindings (verified in IDX Broker 2026-09-09)
| Area | IDX saved link | Status |
|---|---|---|
| Lutz | `lutz` (ID 3053, category `search`) | ✅ exists |
| Wesley Chapel | `wesley-chapel` (ID 3055, category `search`) | ✅ exists — note duplicate ID 2796, retire it |
| Northdale | `northdale` (ID 3054, category `search`) | ✅ exists |
| North Tampa | `north-tampa-suburbs` (ID 3056, category `search`) | ✅ exists |
| Land O' Lakes | — | ❌ **MISSING** a `search`-category link. Must be created before this page is built. Four non-search links exist (`land-o-lakes-new`, `-sold`, `-luxury-lp500000-pt1`, `-luxury-lp1000000-pt1`) |

---

## DRAFTING PROMPT — for Heather and Jeremy, per area
Two or three sentences, in your own words, answering:
- Who actually moves to this area, and what are they usually coming for?
- What's the one thing people get wrong about it, or don't realise until they're here?
- What would you tell a friend who asked whether they should look here?

Not marketing copy. The way you'd answer the question in the car on the way to a showing.

---

## WORKED DRAFT — `/neighborhoods/lutz` (for correction, not publication)
Provided so there's something to react to rather than a blank page.
**Every sentence below must be confirmed or replaced by Team Sid before it ships.**

> **[DRAFT — CONFIRM OR REPLACE]**
> Lutz sits just north of Tampa, close enough that the commute still works and far enough out that
> you get more room than you would closer in. It's the kind of place people move to when they've
> decided they want the yard.
>
> We've watched a lot of families make that trade here, and the ones who are happiest are the ones
> who came out to see it in person first — Lutz reads differently on a map than it does in the car.

Claims made: geography (north of Tampa) only. No prices, no schools, no rankings, no superlatives.
If Team Sid replaces this, hold the same discipline — numbers belong to the widgets.
