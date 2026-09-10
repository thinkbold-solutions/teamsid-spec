# Team Sid — build spec

Machine-readable build specification for the Team Sid website
(Tampa Bay real estate — Lutz, Land O' Lakes, Wesley Chapel, Northdale, North Tampa).

This repository is **public solely so the site builder's web-fetch tool can read it.**
It contains no credentials, no API keys and no private data — every fact in it is already
published on the client's own website.

## Files
| File | Purpose |
|---|---|
| `SPEC.md` | The build specification. Read in full before building. |
| `AGENTS.md` | Governance rules. Re-read on every edit. **AGENTS.md always wins over SPEC.md.** |
| `content/buyers.md` | Literal copy for `/buyers` |
| `content/sellers.md` | Literal copy for `/sellers` |
| `content/neighborhoods.md` | Structure + copy rules for the neighbourhood pages |

## How to use
> Fetch and read this specification in full, then build exactly what it describes.
> Follow every numbered requirement literally. Do not paraphrase any copy.
> Do not add anything not listed.

## Non-negotiables
1. **Third-party embeds render verbatim.** Their output cannot be read at build time. Never
   substitute static content for one, and never infer what one displays.
2. **Never invent facts.** No ratings, reviews, testimonials, listings, MLS numbers, statistics
   or credentials. If data does not exist, omit the element.
3. **Fail loudly.** Never show a success state for a failed submission.
4. **Every control works.** Never render a button or link with no destination.

Maintained by ThinkBOLD Solutions.
