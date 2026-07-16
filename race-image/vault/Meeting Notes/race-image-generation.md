# Race Image Generation

## Overview
End-to-end pipeline for producing the "Sisyphean Race" photorealistic image: six specific people running an exhausting uphill race toward a prize station (MIAL logo statue, FIFA World Cup trophy, glittering BUYME card). The working kit lives in `race-image/` — reference photos in `people/`, web-sourced assets in `assets/`, and the full generation prompt in `PROMPT.md`. The image itself has not been generated yet; generation will run through an external tool (Gemini/ChatGPT via the user's browser, or the OpenAI API). The project is version-controlled at the public GitHub repo `mcleviman-pixel/GRAPHICS` (branch `main`).

## Open Questions
- Final image not yet generated — user is running it manually in ChatGPT/Gemini with the two boards in `race-image/upload/`; save the result to the repo when it arrives
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
