# Podium Video

## Overview
The first video deliverable of the GRAPHICS project: a 30-second celebratory clip (`race-image/output/video/mial-podium-video.mp4`, 1280x720, with stadium-ambience audio) in which each of the six employees stands on a winners' podium receiving a prize, closing with Idit raising the World Cup trophy as the race winner. Produced end-to-end via the OpenAI API (gpt-image-1 stills → Sora 2 image-to-video clips) plus local assembly (ffmpeg concat, GDI+-rendered Hebrew name captions).

## Open Questions
- Awaiting Alon's approval of the toon cut (`mial-podium-toon.mp4`); tweakable: timing, colors, extra celebration moves, music track if supplied

## Session Log

### 2026-07-16 — First cut produced and delivered locally [shipped]
- **What was done:** Confirmed Sora 2 access on the user's OpenAI key; generated 6 podium stills with the proven face-crop likeness pipeline (podium set from [[race-image-generation]] + tight face crops); ran 7 Sora 2 clips (4s each, 1280x720, image-to-video with the stills as first frames): opening establishing shot + one clip per employee; assembled with ffmpeg (installed via winget) — per-clip Hebrew caption overlays rendered locally with GDI+ (RTL via StringFormatFlags.DirectionRightToLeft), 7-segment concat with Sora's own audio. Total ~30.2s.
- **Decisions:** Clip order: opening → Daud → Alon → Dudi → Elinor → Meital → Idit finale ("עידית — המנצחת!"). Hebrew captions rendered locally, never by the AI models. Sora moderation blocked Dudi's first still twice (deterministic on the input image) — regenerating a different still of him passed; lesson: on a Sora input-image block, change the image, not the prompt.
- **Notes / Caveats:** Cost ≈ $4-5 total (6 stills + 8 Sora clip attempts). ffmpeg lives under WinGet packages dir; not on PATH in this session. Sora clips include generated audio — kept as the soundtrack.
- **Related:** [[race-image-generation]], [[brand-assets]], [[sisyphean-race-image-brief]]

### 2026-07-16 — Toon cut: cartoon bodies + real photo faces, new standings [shipped]
- **What was done:** User updated the standings (1. Meital, 2. Dudi, 3. Alon+Idit; Daud and Elinor out) and requested a very simple animation style — cartoon bodies with real photo faces (JibJab style). Built a fully-local GDI+ frame renderer (`render-toon.ps1`, 360 frames @15fps, 24s): flat stadium scene with the real MIAL/BUYME/WC-2026 logo PNGs on the sponsor wall, cartoon podium, oval "sticker" face cutouts, walk-in + hop choreography (Alon+Idit → 3rd, Dudi → 2nd, Meital last → 1st holding a drawn gold trophy and a disproportionate BUYME ALL card labeled "500 ₪" raised overhead), confetti, RTL Hebrew captions, crowd audio reused from the earlier Sora clips. Output: `output/video/mial-podium-toon.mp4`.
- **Decisions:** Zero AI in the animation itself — user said Sora "no longer works" for them and wanted photo-faces that never drift; local rendering guarantees identity and Hebrew text. Giant card held overhead so it never covers other faces (it hid Dudi in the first draft). Jersey colors kept (Idit navy France, others red Spain).
- **Notes / Caveats:** Faces intentionally do not match bodies (user explicitly OK'd). Frame renders live in the session scratchpad only; the repo keeps the final MP4. Meital's card transiently occludes Dudi while she walks past — accepted.
- **Related:** [[race-image-generation]], [[brand-assets]]
