# Brand Assets

## Overview
Sources and usage rules for every brand/visual asset used in the GRAPHICS project, all stored in `race-image/assets/`. Covers the MIAL corporate logo, BUYME gift-card branding, the three national-team jerseys, and the FIFA World Cup trophy reference. All assets were downloaded from their canonical sources and visually verified.

## Open Questions
- none

## Session Log

### 2026-07-16 — Asset sourcing and verification [shipped]
- **What was done:** Downloaded and visually verified all reference assets.
- **Decisions:**
  - **MIAL logo** — `mial-logo.svg` + `mial-logo.png` from the official site (mialimpex.com, WordPress uploads). Diamond/rhombus emblem with "MIAL" letterforms in dark gray `#393839`. In generated imagery it must be reproduced faithfully (statue engraving).
  - **BUYME** — `buyme-card.png` is the BUYME ALL card design (black, gold glitter stars) from buyme.co.il; `buyme-logo.png` is the pelican logo. The "glittering card" in the race image should read as this design.
  - **Jerseys** — Spain 2026 home (adidas, vivid red / navy sleeves; soccerwearhouse.com CDN), Argentina home (adidas, white + sky-blue stripes, AFA crest; FIFA store CDN), France home (Nike, dark navy, FFF rooster; thesoccerfactory.com CDN).
  - **World Cup trophy** — real photograph from Wikimedia Commons; gold body, malachite base.
- **Notes / Caveats:** Retailer CDN links can rot — if an asset is lost, re-source from official federation/brand stores. SVG kept alongside PNG because some AI tools reject SVG uploads.
- **Related:** [[race-image-generation]], [[sisyphean-race-image-brief]]
