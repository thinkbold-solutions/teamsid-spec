# BUILD SPEC — Team Sid, Tampa Bay Real Estate

Build exactly what this specification describes. Every quoted string is literal — do not
paraphrase, improve, shorten or embellish any copy. Do not add sections, images, icons or
content that is not listed here. If information is missing, render an empty state or omit the
element. **Never invent content to fill a gap.**

> Status: v1 — global system + home page complete. Per-route body copy for `/buyers`,
> `/sellers` and the new pages is marked **[COPY PENDING]** and must be supplied before those
> routes are built. Do not generate placeholder copy for them.

---

## 1. HEAD / METADATA — per route

Canonical host: `https://teamsidtampabay.com`. Every route gets its own title, meta description
and self-referencing canonical. **One `<h1>` per page, no exceptions.**

| Route | Title (literal) | Meta description (literal) |
|---|---|---|
| `/` | `Team Sid \| Tampa Bay Real Estate — Homes for Sale in Lutz, Land O' Lakes & Wesley Chapel` | `Tampa Bay real estate experts serving Lutz, Land O' Lakes, Wesley Chapel & Northdale. Search MLS listings, get a free home valuation, and work with a trusted local team. Call (813) 212-8791.` |
| `/about-us` | `Meet Team Sid — Heather & Jeremy Sidlauskas, Tampa Bay Realtors` | `Heather and Jeremy Sidlauskas are a husband-and-wife real estate team with Bay Realty of Florida, serving Lutz, Land O' Lakes, Wesley Chapel and Northdale.` |
| `/about-us/heather` | `Heather Sidlauskas — Tampa Bay Realtor \| Team Sid` | **[COPY PENDING]** |
| `/about-us/jeremy` | `Jeremy Sidlauskas — Tampa Bay Realtor \| Team Sid` | **[COPY PENDING]** |
| `/reviews` | `Client Reviews — Team Sid Tampa Bay Real Estate` | **[COPY PENDING]** |
| `/contact` | `Contact Team Sid — Tampa Bay Real Estate` | **[COPY PENDING]** |
| `/buyers` | `Buying a Home in Tampa Bay \| Buyer's Guide from Team Sid` | `A step-by-step guide to buying a home in Lutz, Land O' Lakes, Wesley Chapel and Northdale, from a local husband-and-wife team.` |
| `/buyers/first-time` | `First-Time Home Buyers in Tampa Bay \| Team Sid` | **[COPY PENDING]** |
| `/buyers/financing` | `Mortgage & Affordability Calculators \| Team Sid Tampa Bay` | **[COPY PENDING]** |
| `/buyers/relocation` | `Relocating to Tampa Bay \| Team Sid` | **[COPY PENDING]** |
| `/sellers` | `Selling Your Tampa Bay Home \| Team Sid` | **[COPY PENDING]** |
| `/sellers/marketing-plan` | `How We Market Your Home \| Team Sid Tampa Bay` | **[COPY PENDING]** |
| `/sellers/cma` | `Free Comparative Market Analysis \| Team Sid Tampa Bay` | **[COPY PENDING]** |
| `/home-valuation` | `What's My Tampa Bay Home Worth? Free Valuation \| Team Sid` | **[COPY PENDING]** |
| `/neighborhoods` | `Tampa Bay Neighborhoods \| Lutz, Land O' Lakes, Wesley Chapel, Northdale` | **[COPY PENDING]** |
| `/neighborhoods/lutz` | `Homes for Sale in Lutz, FL \| Team Sid` | **[COPY PENDING]** |
| `/neighborhoods/land-o-lakes` | `Homes for Sale in Land O' Lakes, FL \| Team Sid` | **[COPY PENDING]** |
| `/neighborhoods/wesley-chapel` | `Homes for Sale in Wesley Chapel, FL \| Team Sid` | **[COPY PENDING]** |
| `/neighborhoods/northdale` | `Homes for Sale in Northdale, FL \| Team Sid` | **[COPY PENDING]** |
| `/neighborhoods/north-tampa` | `Homes for Sale in North Tampa, FL \| Team Sid` | **[COPY PENDING]** |
| `/blog` | `Tampa Bay Real Estate Blog \| Team Sid` | `Market updates, buyer and seller guides, and local insight for Lutz, Land O' Lakes, Wesley Chapel and Northdale.` |
| `/trusted-partners` | `Our Trusted Partners — Team Sid Tampa Bay Real Estate` | `Team Sid's network of trusted lenders, contractors and service professionals across Tampa Bay.` |
| `/privacy-policy` | `Privacy Policy — Team Sid` | (existing copy — port verbatim) |
| `/terms-and-conditions` | `Terms & Conditions — Team Sid` | (existing copy — port verbatim) |
| `/accessibility` | `Accessibility Statement — Team Sid` | **[COPY PENDING]** |
| `/idx-wrapper` | *(see §13 — not a public page)* | `noindex` |

---

## 2. CODE ARCHITECTURE  ← never omit
1. One component per file in `src/components/`, kebab-case filenames.
2. Route files compose components only — no inline markup blocks.
3. All content arrays (nav, footer, partners, FAQ, neighbourhoods) live in `src/lib/content.ts`.
4. All third-party embed snippets live in `src/lib/embeds.ts` as exact strings (§11).
5. Motion primitives in `src/components/motion/reveal.tsx`.

## 3. DESIGN TOKENS (src/styles.css)
6. Primary: `#0069A8` — equivalently `hsl(202 100% 33%)`. Use this exact colour. Convert to the
   template's colour space if required, but the rendered value must match.
7. Primary foreground: `#FFFFFF`.
8. **Exactly two dark surface tokens** — `--surface-dark: #3A3F47`, `--surface-darker: #24282F`.
   Every dark band uses one of these two tokens. Do not introduce additional grey values.
9. `--background: #FFFFFF`, `--foreground: #0F172A`, `--muted-foreground: #64748B`.
10. `--radius: 0.75rem`.
11. Body font: Inter. Display font: Inter (600/700). Load **only** weights 400, 600, 700.
12. Type scale — h1 `clamp(2.25rem, 5vw, 3.75rem)`, h2 `clamp(1.875rem, 3.5vw, 3rem)`,
    h3 `1.25rem`, body `1.0625rem`, line-height 1.6.
13. Section container `mx-auto max-w-6xl px-6`. Section rhythm `py-20` (not `py-24`).

## 4. PERFORMANCE BUDGET  ← never omit
14. Google Fonts: only the weights in §11. No full variable ranges, no italic axis.
    Keep `display=swap` + preconnects.
15. No animation, carousel, charting or icon library beyond those named in §6.
16. No layout shift on load. **Reserve fixed height for every third-party embed in §11** — they
    load asynchronously and will otherwise push content.
17. Target: Lighthouse mobile performance ≥ 90, CLS 0, TBT < 100ms.

## 5. SECTION ORDER — `/` (exact, top to bottom)
18. Header → Hero → Featured Listings (IDX) → Home Valuation → Neighbourhoods →
    Map Search (IDX) → FAQ → Reviews (IDX + Google) → Blog Teasers → Contact → Footer.
    No other sections.

## 6. MOTION
19. Library: `framer-motion`. Single easing `[0.16, 1, 0.3, 1]`.
20. Entrance: opacity 0→1, translateY 24px→0, duration 0.7s.
21. Scroll reveal `once: true`, viewport margin `-80px`, stagger 0.08s.
22. ALL motion disabled under `prefers-reduced-motion: reduce` — render the final state immediately.
23. Content must be **readable with JavaScript disabled**. Do not gate visibility on an
    IntersectionObserver, and never set a section to `opacity: 0` as its default state.

## 7. INTERACTION & ACCESSIBILITY
24. Visible `focus-visible` ring in `--primary` on every interactive element.
25. Semantic heading order, no skipped levels, exactly one `<h1>` per route.
26. Alt text on every image. Skip link to `#main-content`.
27. **Every CTA must have a real destination.** A control with nothing to do must not be rendered.
28. Do not render carousel arrows unless there is more than one item to page through.

## 8. CONTENT (literal)

### 8.1 Global — primary nav
Order and destinations exactly:
`HOME` → `/` · `ABOUT US` → `/about-us` · `BUYERS` → `/buyers` · `SEARCH` → `/search` ·
`NEIGHBORHOODS` → `/neighborhoods` · `SELLERS` → `/sellers` · `HOME VALUATION` → `/home-valuation` ·
`BLOG` → `/blog` · `CONTACT` → `/contact`

### 8.2 Global — footer
29. Business block, exactly:
    `Team Sid` · `(813) 212-8791` · `Info@teamsidtampabay.com`
    `12000 N Dale Mabry Highway, Suite 150-B, Tampa, FL 33618`
    `Broker: Richard Dombrowski` · `Bay Realty of Florida`
30. Legal line, exactly: `© 2026 Team Sid. All rights reserved.`
    Render the current year dynamically.
31. Footer links: `Privacy Policy` → `/privacy-policy`, `Terms & Conditions` →
    `/terms-and-conditions`, `Accessibility` → `/accessibility`.
    There is no `/terms-of-service` route. Do not link to one.
32. `Powered by ThinkBOLD Solutions` → `https://thinkboldsolutions.com/`
33. Equal Housing Opportunity mark. Required for a brokerage.

### 8.3 `/` Hero
34. H1, exactly: `From First Tour to Final Keys, We've Got You Covered.`
35. Subhead, exactly: `Your trusted Tampa Bay real estate experts, dedicated to making your home
    buying or selling journey seamless and successful.`
36. Three CTAs, in order — `Search Homes` → `/search`, `Get Home Value` → `/home-valuation`,
    `Contact Us` → `/contact`.

### 8.4 `/` section headings (literal)
37. `Featured Listings` · `What's Your Home Worth?` · `Explore Tampa Bay Neighborhoods` ·
    `Search Properties by Map` · `Frequently Asked Questions` · `What Our Clients Say` ·
    `From the Blog` · `Get in Touch`

37a. ⚠️ **The heading is `Featured Listings`, NOT "Featured Luxury Listings".** The IDX carousel
     falls through: the agent's own listings first, then the brokerage's, then a fallback. Team Sid
     currently have no active listings of their own, so it renders Bay Realty inventory — which is
     wider than their service areas and spans every price tier (observed 2026-09-10: a $119,900
     one-bed in Clearwater). "Luxury" is a claim the widget cannot guarantee and RULE 1 forbids
     claims we cannot support. §5 already said `Featured Listings`; §37 was the outlier.

### 8.5 Brand-name rule
38. The team is written **`Team Sid`** — two words — everywhere. Never `TeamSid`.
39. The brokerage is **`Bay Realty of Florida`**. Never `TeamSid of Bay Realty`.

### 8.6 `/buyers` and `/sellers` — copy is written
40. Literal copy for both routes is in `content/buyers.md` and `content/sellers.md` in this
    repository. Use it verbatim: every H1, eyebrow, H2, body paragraph, service heading, process
    step, CTA label and href.
41. Both pages are **first-person plural** throughout. Never "I".
42. Place names are literal: `Lutz, Land O' Lakes, Wesley Chapel, Northdale and North Tampa`.
    Never emit a sentence containing an unfilled placeholder. If a place name is required and not
    supplied, stop and ask rather than leaving a gap or substituting the business name.

### 8.7 Neighbourhood pages
43. Structure, widget slots and copy rules are in `content/neighborhoods.md`. Follow it exactly.
44. **Every number on those pages comes from a live widget, never from prose.** Do not write
    median prices, school ratings, population figures, commute times or "best of" claims.
45. Intro copy marked `[LOCAL — TEAM SID]` must be supplied by the client. Do not generate it.
46. `/neighborhoods/land-o-lakes` is **blocked** until its `search`-category IDX saved link exists.
    Do not build that route against a different link.

### 8.8 Remaining routes — [COPY PENDING], do not generate
47. Body copy for `/about-us/heather`, `/about-us/jeremy`, `/reviews`, `/contact`,
    `/buyers/first-time`, `/buyers/financing`, `/buyers/relocation`, `/sellers/marketing-plan`,
    `/sellers/cma`, `/home-valuation` and `/accessibility` is **not yet written**. Do not draft,
    infer or placeholder it. If asked to build one of those routes before its copy exists, stop
    and say so.

## 9. CRM INTEGRATION & TRACKING  ← never omit
41. Every form submits through the native CRM form skill so leads create real contacts in the
    connected sub-account with full attribution. **No custom fetch, no tracking-endpoint POST.**
    > Do not POST form data to an analytics or attribution endpoint. That path does not create a
    > contact. Use the native CRM form skill only.
42. Forms and required fields:
    - Contact — First name*, Last name*, Email*, Phone, Message*
    - Home valuation — Property address*, Email*, Phone
    - CMA request — Property address*, Email*, Phone, Timeframe
43. **Fail loudly.** On a failed submission show a visible error including the HTTP status and
    the phone number `(813) 212-8791`. Never show a success state for a failed submission.
44. Analytics in the root document:
    - GA4 measurement ID: `G-74MJ8N06P8`
    - GTM container: **[PENDING — confirm with client]**
    - Meta Pixel: **[PENDING — confirm with client]**
45. Nothing else may be injected into the document head.

## 10. STRUCTURED DATA
46. JSON-LD `RealEstateAgent` at `@id` `https://teamsidtampabay.com/#organization`:
    name `Team Sid` · url `https://teamsidtampabay.com` · telephone `+1-813-212-8791` ·
    email `Info@teamsidtampabay.com`
    address: `12000 N Dale Mabry Highway, Suite 150-B`, `Tampa`, `FL`, `33618`, `US`
    parentOrganization: `Bay Realty of Florida`, `https://www.bayrealtyofflorida.com`
    areaServed: `Lutz`, `Land O' Lakes`, `Wesley Chapel`, `Northdale`, `Tampa` (all `FL`)
    employee: `Heather Sidlauskas` (Realtor), `Jeremy Sidlauskas` (Realtor)
    sameAs: `https://www.facebook.com/HeatherSellsTampaBay/`,
    `https://www.instagram.com/teamsidtampabay`
47. **No `aggregateRating`, no `review`, no `award`, no `numberOfEmployees`** — none of it is
    verified. Only fields listed in §46.

## 11. THIRD-PARTY EMBEDS — render verbatim  ← the most important section
48. The following are `<script>` tags whose content is fetched at runtime from a third party.
    **Render each exactly as given. You cannot read what they output. Never substitute static
    content for one. Never infer what one renders. Never "improve" one.**

    a. Map search — `/` and `/search`
       `https://idxaddons.com/addon/map/b3NhMm5YczVHVlY%3D7_9BcdV_iw8`
    b. Featured listing carousel — `/` — ⚠️ **THE `id` IS FUNCTIONALLY REQUIRED.** This widget
       calls `idx('#idxwidgetsrc-43491')` to find its OWN script tag and inserts the carousel
       beside it. Without the id it executes and renders nothing, silently. Render the COMPLETE
       tag, not just the src:
       `<script charset="UTF-8" type="text/javascript" id="idxwidgetsrc-43491" src="https://idxaddons.com/addon/speedy/b3NhMm5YczVHVlY%3D7_9BcdV_iw8/?w=340&h=0&imgType=2&theme=zoom&site=https%3A%2F%2Fhomes.teamsidtampabay.com%2Fidx%2Fcarousel.php%3Fwidgetid%3D43491"></script>`
       (Only this embed needs an id. The map and testimonials embeds must NOT be given one.)
    c. Testimonials — `/` and `/reviews`
       `https://idxaddons.com/addon/testimonials/b3NhMm5YczVHVlY%3D7_9BcdV_iw8/`
    d. Home valuation — `/home-valuation`
       `https://idxaddons.com/addon/plunkvaluation/b3NhMm5YczVHVlY%3D7_9BcdV_iw8`
    e. CRM reviews widget — ⏸️ **DEFERRED, REMOVED FROM THE SITE 2026-09-10. DO NOT RE-ADD YET.**
       `https://backend.leadconnectorhq.com/appengine/reviews/get_widget/`
       Verified in the CRM 2026-09-10: **no review widget has ever been created**
       (Reputation → Widgets → Saved Widgets is empty) and the account has **ZERO reviews**
       ("No Reviews Yet"), with Google Business Profile not connected. The URL returns **HTTP 404
       with a JSON body**, which the browser then blocks under CORB. It is not a bad URL we
       transcribed — there is nothing behind it. Creating a widget today would render an empty box.
       Removed from `/` under RULE 6 (do not render a control with nothing to do); the Testimonials
       column now runs full width and carries a real IDX testimonial.
       **Bring it back only when BOTH are true:** (1) Google Business Profile is connected and the
       account has real reviews, and (2) a widget has been created under Reputation → Widgets,
       which yields the correct embed URL — this bare path is not it.
49. Additional embeds (Google Reviews, community widgets, calculators, CMA, Property AI, Single
    Property Websites) will be added here once configured. **[PENDING]** — do not invent them.
50. Reserve a fixed-height container for each embed so it cannot cause layout shift (§16).
50a. **Record and render each embed as its COMPLETE tag, never just the `src`.** Attributes such as
     `id` and `charset` can be functionally required — the carousel above renders nothing without
     its `id`. Any injector that builds a script element must copy EVERY attribute, not just `src`,
     or the requirement is silently dropped.
50b. **Third-party widgets must be injected client-side into a container React never reconciles.**
     Server-rendering them via `dangerouslySetInnerHTML` lets the browser execute the script during
     parse, then React hydration wipes the DOM the widget wrote. Symptoms: `Map: Expected mapDiv
     ... passed null`, React error #418. Put the URL in a `data-embed-src` attribute if it must stay
     verifiable in served HTML — this supersedes any reading of §14 items 60/63 that would require
     an executing `<script>` in the SSR output.

## 12. PROHIBITIONS  ← never omit
51. No invented ratings, star graphics, review counts, testimonials, statistics, listings, MLS
    numbers, prices, awards, certifications, years-in-business, client names or team members.
52. **No hard-coded property listings of any kind.** Listings come only from the embeds in §11.
    > Hard-coding listings is stale by design and an IDX compliance problem.
53. No stock photography. No emoji. No "five star" graphics.
54. No routes beyond those listed in §1.
55. If any requirement here conflicts with `AGENTS.md`, **AGENTS.md wins — say so and stop.**

## 13. THE IDX WRAPPER PAGE  ← required for the IDX integration
56. Create a route `/idx-wrapper` containing the full site header and footer, and between them,
    as direct children of `<main>`, in this order, exactly:
    `<div id="idxStart" style="display:none"></div>` and `<div id="idxStop" style="display:none"></div>`
    ⚠️ **DIV ELEMENTS, NOT HTML COMMENTS.** Confirmed by IDX Broker support (RealtyCandy),
    2026-09-10: *"The issue stems from the idxStart and idxStop tags being formatted as HTML
    comments. When present as comments, the wrapper parser misses them."* The comment form
    `<!--idxStart-->` is what every generic IDX Broker guide shows and it does NOT work here —
    their wrapper generator rejects the page with "Please check if your wrapper page has the
    IDXStart and IDXStop tags" even when the comments are provably present in the served HTML.
    ids are case-sensitive: `idxStart` / `idxStop`.
    Bonus: plain JSX, so no `dangerouslySetInnerHTML` and none of the hydration risk in §50b.
57. Nothing between those two markers. IDX Broker injects its page content there.
58. `/idx-wrapper` must be `noindex, nofollow` and must not appear in the nav, footer or sitemap.
59. It must be reachable on the published domain — the wrapper generator cannot read a preview URL.

## 14. VERIFICATION (checked after build — never trust the self-report)
60. Every literal string in §8 present in the **served HTML** (SSR, not post-hydration).
61. Tokens per §3 in `src/styles.css`; exactly two dark surface tokens, not four.
62. Section order per §18. Component/file structure per §2.
63. All five embeds in §11 present **verbatim**, character for character.
64. GA4 from §44 present **and firing** — check the network tab, not the markup.
65. Every CTA resolves to a real destination. Zero dead controls.
66. A test submission on every form creates a real contact in the CRM sub-account.
67. A forced failed submission renders a visible error, not a success state.
68. Lighthouse mobile ≥ §17 targets.
69. Zero fabricated content per §51-§54.
70. `/idx-wrapper` reachable and containing both markers.

## 15. IMAGE ASSETS — the only images permitted  ← added 2026-09-10
The prohibition in the header ("do not add images") and §53 ("no stock photography") stand.
This section is the **allow-list exception**: these files, and only these, may be used. Every one
is the client's own upload, identifiable by the locationId `5ScCH7Aeywc8YnNrNGt1` in its path.
Use the alt text given — it is the client's own, not invented.

71. **Header logo** — natural size 350x180 (**1.94:1**). Render 85x44, or height + width:auto.
    `loading="eager"`. NEVER force a square or any other ratio — 44x44 and 220x60 both squash it.
    `https://assets.cdn.filesafe.space/5ScCH7Aeywc8YnNrNGt1/media/68e5459484a71d0da8e1754c.png`
    alt: `Team Sid Logo`
72. **Footer combined logo** — natural size 350x180 (**1.94:1**). Render 155x80. Lazy.
    `https://storage.googleapis.com/msgsndr/5ScCH7Aeywc8YnNrNGt1/media/69134a6229bad1108098a3fe.webp`
    alt: `Team Sid and Bay Realty of Florida combined logo`
73. **Team photo**, `/about-us` — lazy
    `https://storage.googleapis.com/msgsndr/5ScCH7Aeywc8YnNrNGt1/media/69610a5a15e9b5e1ca6e85e5.webp`
    alt: `Team Sid - Heather and Jeremy Sidlauskas, Tampa Bay Real Estate Experts`
74. **Heather headshot**, `/about-us` — 400x600, lazy
    `https://storage.googleapis.com/msgsndr/5ScCH7Aeywc8YnNrNGt1/media/69137c269e0b185115d3f92f.webp`
    alt: `Heather Sidlauskas`
75. **Jeremy headshot**, `/about-us` — 400x600, lazy
    `https://storage.googleapis.com/msgsndr/5ScCH7Aeywc8YnNrNGt1/media/69137c84042d13f580bae4cf.webp`
    alt: `Jeremy Sidlauskas`
76. Headshots carry the person's NAME as a caption and nothing else. No bio, title, credential,
    years of experience or specialty — that copy does not exist. Do not link them to
    `/about-us/heather` or `/about-us/jeremy`; those routes are [COPY PENDING] (§8.8).
77. Every image needs explicit width/height or an aspect-ratio box (§50, no layout shift) and alt
    text (§26). **The width:height you set must match the asset's natural ratio.** Both logos are
    350x180 = 1.94:1; the headshots are 400x600 = 2:3. A mismatched pair silently distorts the art.
78. **Nothing may be server-rendered at `opacity:0`.** RULE 10 requires content readable with
    JavaScript disabled. Motion wrappers must SSR their final visible state and animate only as a
    progressive enhancement after hydration.

### 15.2 HERO BACKGROUND VIDEO — homepage only
79. **Video** (960x540, h264, 10s loop, no audio, 0.42 MB):
    `https://assets.cdn.filesafe.space/5ScCH7Aeywc8YnNrNGt1/media/6aa23af0bfc1456f8c969b04.mp4`
    **Poster** (0.08 MB) — this is the LCP element and paints first:
    `https://assets.cdn.filesafe.space/5ScCH7Aeywc8YnNrNGt1/media/6aa23b11dd867dc12d09229e.jpg`
80. Decorative background layer behind the hero content. `aria-hidden="true"`. It must not alter
    the §5 section order or move the locked H1.
81. `preload="none"` · `muted` · `playsinline` · `loop` · no controls. It must NOT download during
    initial page load — the poster is what paints.
82. Autoplay ONLY under `prefers-reduced-motion: no-preference`. Under `reduce`, do not autoplay and
    do not load the video at all; leave the poster (RULE 10).
83. Fixed aspect-ratio box, `object-fit: cover`, so it cannot cause layout shift (RULE 7).
84. A dark scrim sits between video and text so the H1/subtitle keep their contrast.
85. **Never use the 5.82 MB original** `.../media/6930b4034d01f36c14a8f6b1.mp4`. It is 22.9s at
    2.13 Mbps — roughly 37x the whole JS bundle — and autoplaying it competes with first paint on an
    LCP that is already the weak point (~3.4s). The file above is that source, trimmed to 10s,
    scaled to 960w, audio stripped: 93% smaller.

### 15.1 BANNED SOURCES — verified stock / AI, never use
78. **`vibe.filesafe.space/1776639819036901291/assets/*`** — 10 decorative images left in the
    abandoned earlier build. 800x533 / 800x640 are stock-library export sizes; 1408x768 PNGs are
    AI-generation output. One of them shows a **wooden chalet with conifers and autumn deciduous
    trees** — northern Europe or the Pacific Northwest, not Tampa Bay, on a Tampa Bay realtor's
    site. Misleading as well as non-compliant.
79. **`res.cloudinary.com/dscqcqtjn/.../five-stars-7292866_1920_bppsf4.png`** — a Pixabay stock
    five-star graphic. This is the exact artefact §53 names and a direct RULE 1 breach.
80. Not-yet-placed client assets, listed so they are not mistaken for stock:
    `.../media/691372619ba8fe816e091537.webp` and `.../media/69e56a3438381eafa8a8dd56.webp`
    (two more compressions of the team photo) and `.../media/6930b4034d01f36c14a8f6b1.mp4` (video).
