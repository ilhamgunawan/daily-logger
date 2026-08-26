---
name: enhance-draft
description: Convert a selected raw draft log (logs/<year>/<month>/drafts/draft_YYYY-MM-DD.md) into a finalized daily entry (logs/<year>/<month>/YYYY-MM-DD.md) following this repo's format and enhancement rules. Use when the user says "enhance draft", "finalize <date>", "generate the log for <date>", or points at a specific draft_*.md file.
---

# Enhance Draft → Final Daily Log

Convert one raw draft into a finalized daily log entry for this repository.
This skill implements the "Enhance draft" workflow described in `AGENTS.md`
and `README.md`.

## Inputs

Determine the target date from the user's request (a date, "today", "the
latest draft", or an explicit path). If ambiguous or multiple unresolved
drafts exist, ask which one to process rather than guessing.

## Steps

1. **Read the rules first.** Load, in order:
   - `docs/format.md` — required frontmatter and section structure.
   - `docs/enhancement-rules.md` — draft-to-final conversion rules.
   - `examples/2026-08-15.md` and `examples/draft_2026-08-15.md` — reference
     pair for tone, level of detail, and STAR-block style.

2. **Locate the draft.** It lives at
   `logs/<year>/<month>/drafts/draft_YYYY-MM-DD.md`. If it doesn't exist,
   stop and tell the user — do not fabricate a draft.

3. **Check for an existing final entry** at
   `logs/<year>/<month>/YYYY-MM-DD.md`. If one already exists, stop and ask
   before overwriting — per the "one pass" rule, an already-final file is
   not rewritten unless explicitly requested.

4. **Read the draft's raw notes** in full.

5. **Convert to the final entry**, applying `docs/enhancement-rules.md`:
   - Never fabricate — every fact must trace back to the draft; mark
     genuinely missing details `(needs detail)`.
   - Preserve every meaningful fact from the draft; merge duplicates, drop
     nothing.
   - Group notes into categories (work, learning, personal, health, social,
     errands) only when more than one note falls in a category.
   - Give each major activity (≥30 min focus, or a notable outcome) its own
     STAR block in `Day in detail`, ordered by significance then
     chronology; fold quick tasks into `Accomplishments` bullets instead.
   - Keep the draft's own voice and level of detail — do not inflate small
     wins into bigger ones.
   - Preserve any timestamps from the draft as written.
   - Follow `docs/format.md` section order exactly: `Summary`,
     `Accomplishments`, `Learnings` (if any), `Blockers / Next steps` (if
     any), `Day in detail`. Empty required sections get `_None._`; optional
     sections with nothing to say are omitted entirely.
   - Build frontmatter per `docs/format.md`: `date`, `weekday`, `status:
     final`, `tags` (2-6 lowercase keywords), `mood`/`energy` (only if
     present in the draft), `generated_from` (relative path to the draft).

6. **Write the final file** to `logs/<year>/<month>/YYYY-MM-DD.md`.

7. **Do not delete the draft.** Only remove it if the user explicitly asks.

8. **Do not commit or push.** Only do so if the user explicitly asks,
   per `AGENTS.md`.

## Output

Report which draft was converted and where the final file was written. If
any `(needs detail)` placeholders were used, call them out explicitly so the
user can fill them in later.
