# GRAPHICS Project

Graphics/image-generation project for MIAL. Remote: https://github.com/mcleviman-pixel/GRAPHICS (public, branch `main`).

## Mandatory: Obsidian Vault Workflow — every session, every task

This project's long-term memory is the Obsidian vault at `race-image/vault/`.

**At the START of every task** (including the first command of a session) and **at the END of every task**, follow the protocol in the `obsidian-vault-workflow` skill (`.claude/skills/obsidian-vault-workflow/SKILL.md`):

- START: identify the topic, check the folder `_index.md`, read the matching topic file fully, read the 2–3 most recent Meeting Notes, and state what context was loaded.
- END: append a dated `### YYYY-MM-DD — <title> [status]` entry to the topic file's Session Log, update Overview/Open Questions if needed, keep `_index.md` in sync, and verify by reading back.

Skip only for pure read-only questions that touch zero files and produce zero decisions.

## Vault conventions

- Vault root: `race-image/vault/` (folders: `Meeting Notes/`, `Content Briefs/`, `Publishing Log/`, `Brand Guidelines/`).
- All vault files use Obsidian Flavored Markdown — follow the `obsidian-markdown` skill (wikilinks `[[topic]]`, not markdown links, for intra-vault references).
- For database-like views (`.base` files), follow the `obsidian-bases` skill.

## Notes

- `race-image/` is the "Sisyphean Race" image kit: `people/` (reference photos), `assets/` (brand/jersey/trophy images), `PROMPT.md` (generation prompt), `README.md` (Hebrew usage guide).
- Commit and push to `origin main` after completing meaningful work in this repo.
