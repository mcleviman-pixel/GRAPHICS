# Race Image Generation

## Overview
End-to-end pipeline for producing the "Sisyphean Race" photorealistic image: six specific people running an exhausting uphill race toward a prize station (MIAL logo statue, FIFA World Cup trophy, glittering BUYME card). The working kit lives in `race-image/` — reference photos in `people/`, web-sourced assets in `assets/`, and the full generation prompt in `PROMPT.md`. The image itself has not been generated yet; generation will run through an external tool (Gemini/ChatGPT via the user's browser, or the OpenAI API). The project is version-controlled at the public GitHub repo `mcleviman-pixel/GRAPHICS` (branch `main`).

## Open Questions
- User must pick a final version from `race-image/output/` (v1/v2/v3) or request another refinement round
- The MIAL logo text on the statue never renders correctly (v1: abstract, v2: "M", v3: "HAL") — likely needs a local post-processing overlay of the real logo PNG instead of more generation rounds
- Meital is still not clearly present as a second woman in red in v3
- The OpenAI API key sits in the session scratchpad (`openai.key`) — remind the user to delete the key at platform.openai.com when iteration is done
- Idit's reference photos are imperfect (sunglasses in one, cap + second person in the other) — a clean frontal photo would improve likeness

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
