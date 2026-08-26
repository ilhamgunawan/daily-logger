---
name: summarize-week
description: Generate a weekly summary (logs/<year>/<month>/summary_<year>-W<ISO>.md) from a week's finalized daily entries, following this repo's summary rules. Use when the user says "summarize the week", "generate weekly summary", "weekly summary for <date/week>", or names an ISO week.
---

# Summarize Week

Produce one ISO-week summary from that week's finalized daily logs. This
skill implements the weekly part of the "Summarize" workflow described in
`AGENTS.md` and `README.md`.

## Inputs

Determine the target ISO week from the user's request (an explicit
`YYYY-Www`, a date that falls in the week, or "this week"/"last week"). If
ambiguous, ask which week to summarize rather than guessing.

## Steps

1. **Read the rules first.** Load `docs/summary-rules.md` in full — it
   defines file naming, frontmatter, and the weekly section structure.

2. **Resolve the week boundaries.** Weeks are ISO 8601: Monday–Sunday, week
   number = ISO week (e.g. `2026-W33`). Compute the Monday and Sunday dates
   for the target week.

3. **Check the week has ended.** A weekly summary must not be created until
   its week has ended (i.e. today's date is after that week's Sunday). If
   the week is still in progress, stop and tell the user.

4. **Collect the week's final entries.** For each day Monday–Sunday, look
   for `logs/<year>/<month>/YYYY-MM-DD.md`. Use **only** final entries —
   never drafts. If a day has no final entry, treat it as unlogged (do not
   fabricate content for it) and note the gap if relevant, but continue
   with the days that do exist. If **no** final entries exist for the week,
   stop and tell the user instead of producing an empty summary.

5. **Determine the destination path.** A weekly summary lives in the month
   folder containing the week's **Monday**:
   `logs/<year>/<month>/summary_<year>-W<ISO>.md`. If the week straddles two
   months, still account for final logs from both months in the content,
   but store the file only once, under Monday's month.

6. **Check for an existing summary** at that path. If one already exists,
   stop and ask before overwriting.

7. **Read each collected final entry in full** (frontmatter + all
   sections).

8. **Build the summary**, applying `docs/summary-rules.md`:
   - Frontmatter: `date: YYYY-MM-DD..YYYY-MM-DD` (Monday..Sunday),
     `status: weekly`, `source_logs` listing every final path used.
   - `## Overview` — 1-2 paragraphs on the week's theme and overall tone.
   - `## Highlights` — day-by-day, one line each:
     `YYYY-MM-DD (Weekday): <2-3 bullets>`.
   - `## Trends` — recurring topics across the week (work, energy, mood),
     each with an evidence tag (e.g. `2026-08-15.md`).
   - `## Blockers` — blockers carried from daily logs, with resolution
     status if any changed during the week.
   - `## Next week focus` — 2-5 concrete `- [ ]` items, drawn from unresolved
     next-steps in the daily logs.
   - Cite sources inline as `YYYY-MM-DD.md` or `YYYY-MM-DD.md#section`.
   - Never introduce a fact absent from the final logs used.

9. **Write the summary file** to the destination path from step 5.

10. **Do not commit or push.** Only do so if the user explicitly asks, per
    `AGENTS.md`.

## Output

Report the ISO week summarized, which final entries were used as sources
(and which days, if any, had no final entry), and where the summary file
was written.
