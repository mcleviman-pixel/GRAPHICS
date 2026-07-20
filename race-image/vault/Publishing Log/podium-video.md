# Podium Video

## Overview
The first video deliverable of the GRAPHICS project: a 30-second celebratory clip (`race-image/output/video/mial-podium-video.mp4`, 1280x720, with stadium-ambience audio) in which each of the six employees stands on a winners' podium receiving a prize, closing with Idit raising the World Cup trophy as the race winner. Produced end-to-end via the OpenAI API (gpt-image-1 stills → Sora 2 image-to-video clips) plus local assembly (ffmpeg concat, GDI+-rendered Hebrew name captions).

## Open Questions
- Awaiting Alon's approval of the final cut; possible refinements: Alon/Elinor hold a generic golden trophy instead of a MIAL statue; background music could be added if a licensed track is supplied

## Session Log

### 2026-07-16 — First cut produced and delivered locally [shipped]
- **What was done:** Confirmed Sora 2 access on the user's OpenAI key; generated 6 podium stills with the proven face-crop likeness pipeline (podium set from [[race-image-generation]] + tight face crops); ran 7 Sora 2 clips (4s each, 1280x720, image-to-video with the stills as first frames): opening establishing shot + one clip per employee; assembled with ffmpeg (installed via winget) — per-clip Hebrew caption overlays rendered locally with GDI+ (RTL via StringFormatFlags.DirectionRightToLeft), 7-segment concat with Sora's own audio. Total ~30.2s.
- **Decisions:** Clip order: opening → Daud → Alon → Dudi → Elinor → Meital → Idit finale ("עידית — המנצחת!"). Hebrew captions rendered locally, never by the AI models. Sora moderation blocked Dudi's first still twice (deterministic on the input image) — regenerating a different still of him passed; lesson: on a Sora input-image block, change the image, not the prompt.
- **Notes / Caveats:** Cost ≈ $4-5 total (6 stills + 8 Sora clip attempts). ffmpeg lives under WinGet packages dir; not on PATH in this session. Sora clips include generated audio — kept as the soundtrack.
- **Related:** [[race-image-generation]], [[brand-assets]], [[sisyphean-race-image-brief]]
