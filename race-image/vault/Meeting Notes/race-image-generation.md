# Race Image Generation

## Overview
End-to-end pipeline for producing the "Sisyphean Race" photorealistic image: six specific people running an exhausting uphill race toward a prize station (MIAL logo statue, FIFA World Cup trophy, glittering BUYME card). The working kit lives in `race-image/` — reference photos in `people/`, web-sourced assets in `assets/`, and the full generation prompt in `PROMPT.md`. The image itself has not been generated yet; generation will run through an external tool (Gemini/ChatGPT via the user's browser, or the OpenAI API). The project is version-controlled at the public GitHub repo `mcleviman-pixel/GRAPHICS` (branch `main`).

## Open Questions
- Mud-race edit rejected: user wants everyone except Idit pixel-identical to the original photo. Planned pipeline (paused mid-approval): DALL-E 2 true inpainting for the tall-man removal + manual head composite for Idit + local bib text. Resume if the user asks.
- Awaiting user verdict on `output/podium-v1.png`; offer pixel-perfect local logo overlay if needed
- Podium video produced — see [[podium-video]] in Publishing Log; awaiting user approval
- The OpenAI API key sits in the session scratchpad (`openai.key`) — remind the user to delete the key at platform.openai.com when iteration is done

## Session Log

### 2026-07-16 — Asset kit, prompt, GitHub setup [wip]
- **What was done:** Built the full `race-image/` kit: downloaded and visually verified all web assets (MIAL logo SVG+PNG from mialimpex.com, Spain/Argentina/France jerseys from retailer CDNs, World Cup trophy from Wikimedia, BUYME ALL card design + pelican logo from buyme.co.il); wrote `PROMPT.md` (detailed English photorealistic prompt) and `README.md` (Hebrew instructions); received and renamed all 7 people photos; initialized git and pushed everything to `mcleviman-pixel/GRAPHICS`.
- **Decisions:** Idit must be unmistakably first (user requirement); order of the other five runners is free. Jerseys: Idit=France, Daud=Argentina, Alon/Dudi/Elinor/Meital=Spain. Both Idit photos kept as dual reference (`idit.jpeg`, `idit-2.jpeg`) with an explicit prompt instruction to ignore the bald man in `idit-2` and render her without cap/sunglasses. User explicitly approved pushing the personal photos to the public repo. `.claude/settings.local.json` excluded from git via `.gitignore`.
- **Notes / Caveats:** No image-generation capability in this environment — generation must go through an external tool. Chrome extension was unreachable when attempted; no MCP connectors installed.
- **Related:** [[sisyphean-race-image-brief]], [[brand-assets]]

### 2026-07-16 — Manual generation kit (labeled boards) [wip]
- **What was done:** Built `race-image/upload/` for the manual generation path: two labeled contact sheets composed with PowerShell + System.Drawing (`board-people.jpg` — all 7 runner photos with name+jersey labels; `board-assets.jpg` — jerseys, trophy, MIAL logo, BUYME card+logo with labels), plus `INSTRUCTIONS.md` with a 3-step Hebrew guide and a board-adapted English prompt.
- **Decisions:** Manual path chosen because the user is on Edge and the Claude browser extension is Chrome-only (a regular-Claude extension got installed by mistake; Claude Code pairing unavailable). Two merged boards instead of 15 separate files — most AI chat tools cap attachments at ~10 images and filenames are lost on upload, so labels are baked into the images.
- **Notes / Caveats:** Boards verified visually. If a runner's likeness comes out weak, fall back to attaching that person's original photo from `people/` alongside the boards.
- **Related:** [[sisyphean-race-image-brief]], [[brand-assets]]

### 2026-07-16 — First generations via OpenAI API (v1–v3) [wip]
- **What was done:** User funded an OpenAI account and provided an API key; generated three iterations with `gpt-image-1` via the `/v1/images/edits` endpoint (multipart curl, both labeled boards as reference images, size 1536x1024, quality high). Results in `race-image/output/race-v1..v3.png`. v1: composition and mood right, Idit clearly first; but one runner wore a gray tee, statue logo mangled, card read "BUYNE". v2: card fixed to "BUYME"+pelican; statue only "M"; lost one of the two women in red. v3: Daud clearly visible, but statue reads "HAL" and Meital still missing as a second red-jersey woman.
- **Decisions:** Refinements chain the previous output as the first input image plus both boards — keeps composition stable while fixing specifics. API key stored only in the session scratchpad (`openai.key`), never in the repo.
- **Notes / Caveats:** gpt-image-1 cannot reliably render the small "MIAL" lettering — plan B is compositing the real logo PNG onto the statue locally (System.Drawing overlay, same technique as the boards). Gender/person drift appears when swapping runners; targeted single-change prompts work better than multi-fix prompts.
- **Related:** [[sisyphean-race-image-brief]], [[brand-assets]]

### 2026-07-16 — v4: individual face refs + front-facing prizes [wip]
- **What was done:** User reported v1–v3 likenesses were weak and the prize station looked like it was seen from behind. Root cause for likeness: the contact-sheet boards shrink each face to a small cell. Fix: sent the six ORIGINAL photos individually (full resolution, ordinal references in the prompt) plus the assets board; made local face crops with System.Drawing for Idit (left woman only from `idit-2`, excluding the bald man) and Meital (zoom from the group photo) — saved in `people/crops/`. Prompt now demands the pedestal be angled with all prize fronts toward the camera. Result `output/race-v4.png`: statue reads "MIAL", card reads "BUYME", all six jerseys correct (1 France + 1 Argentina + 4 Spain incl. both women), Idit clearly first, faces far closer to the references.
- **Decisions:** Individual full-res photos with ordinal prompt references beat labeled contact sheets for identity fidelity; boards remain useful only for props/wardrobe. Fresh generation (not chained edit) when likeness needs rebuilding.
- **Notes / Caveats:** Verified the prize-station text by zoom-cropping v4. Meital's glasses kept per her reference photo.
- **Related:** [[sisyphean-race-image-brief]], [[brand-assets]]

### 2026-07-16 — v5: tight-crop face replacement round [wip]
- **What was done:** User said only Meital resembled her reference in v4. Key insight: Meital was the only runner whose reference was a tight face close-up — identity fidelity tracks how much of the reference frame the face fills. Made tight head crops for the other five (`people/crops/*-tight.jpg`, System.Drawing), then ran an edits round on v4: keep scene/prizes/jerseys, replace only the five faces (Meital untouched). Result `output/race-v5.png`; prize texts survived (zoom-verified: "MIAL" statue, "BUYME" card with pelican).
- **Decisions:** Reference photos must be tight face crops — codify for all future person-likeness work. Dudi's only photo has cap+sunglasses; prompt describes his visible features and instructs bare head, likeness is best-effort.
- **Notes / Caveats:** Daud's goatee weakened in v5 vs v4; if the user flags him, re-run a single-person fix with `daud-tight.jpg`.
- **Related:** [[sisyphean-race-image-brief]], [[brand-assets]]

### 2026-07-16 — Mud-race image: pivot to user-supplied base, hybrid AI+local pipeline [shipped]
- **What was done:** User rejected the desert scene and supplied a new mud-race base photo (`input/`), asking to (1) delete the tall long-haired man at the back, (2) improve Idit, (3) fix her bib "רודית"→"עידית". After failed attempts (v6: model removed an extra man and put glasses on Idit; masked inpaint v8a: gpt-image-1 masks are soft guidance, whole image regenerated; local rectangle compositing: model output is not geometrically aligned with input), the working pipeline was: v10 full edit (remove man + Idit face from `idit-tight.jpg` ref), v11 single-change edit (remove the glasses the model kept adding to Idit), then LOCAL System.Drawing repaint of all three Hebrew bibs (עידית/דאוד/אלינור) — sampled bib yellow, noise speckle, Arial Bold Hebrew. Final: `output/race-final.png`.
- **Decisions:** Hebrew text in gpt-image-1 is hopeless — always restore text locally. gpt-image-1 has no true inpainting (mask ≈ suggestion) and outputs are never pixel-aligned with inputs, so patch-compositing between generations does not work; chain single-change edits instead. PS 5.1 scripts containing Hebrew must be written UTF-8 **with BOM**.
- **Notes / Caveats:** Failed intermediates (v7a, v8a, v9-composite) deleted. The model repeatedly migrated Meital's glasses onto Idit — explicit "she has NO glasses / the OTHER woman keeps hers" wording is what finally worked.
- **Related:** [[sisyphean-race-image-brief]], [[brand-assets]]

### 2026-07-16 — Podium image with three logos [shipped]
- **What was done:** New request: podium image with the MIAL, BUYME, and FIFA World Cup 2026 logos. (User also rejected `race-final.png` — they want the mud-race photo with everyone except Idit pixel-identical to the original; that thread is paused, see Open Questions.) Downloaded the official 2026 emblem (Wikipedia, `assets/worldcup-2026-logo.png`), generated with gpt-image-1 using the three logo PNGs as references: three-tier podium (1-2-3) on a stadium pitch at dusk, sponsor backdrop wall carrying all three logos. First attempt (`output/podium-v1.png`) came out clean — BUYME pelican+wordmark near-perfect, FIFA emblem good, MIAL monogram close to original and legible.
- **Decisions:** Sponsor-wall composition chosen because a flat camera-facing banner keeps logos crisp and allows pixel-perfect local overlay of the real PNGs if ever needed.
- **Notes / Caveats:** Tiny garble on the trophy's green base band; MIAL monogram styling approximate. Offer local overlay if the user wants exact logos.
- **Related:** [[brand-assets]], [[sisyphean-race-image-brief]]
