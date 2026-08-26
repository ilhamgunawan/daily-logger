---
name: summarize-month
description: Generate a monthly summary (logs/<year>/<month>/summary_<year>-<month>.md) from a month's finalized daily entries (and that month's weekly summaries where useful), following this repo's summary rules. Use when the user says "summarize the month", "generate monthly summary", "monthly summary for <year>-<month>", or names a month.
---

# Summarize Month

Produce one monthly summary from that month's finalized daily logs. This
skill implements the monthly part of the "Summarize" workflow described in
`AGENTS.md` and `README.md`.

## Inputs

Determine the target month from the user's request (`YYYY-MM`, a month
name + year, or "this month"/"last month"). If ambiguous, ask which month
to summarize rather than guessing.

## Steps

1. **Read the rules first.** Load `docs/summary-rules.md` in full — it
   defines file naming, frontmatter, and the monthly section structure.

2. **Check the month has ended.** A monthly summary should reflect a
   complete month. If the target month is the current, still-in-progress
   month, stop and confirm with the user before proceeding (they may
   explicitly want a partial-month summary).

3. **Collect the month's final entries.** Look for every
   `logs/<year>/<month>/YYYY-MM-DD.md` in the target month. Use **only**
   final entries — never drafts. If **no** final entries exist for the
   month, stop and tell the user instead of producing an empty summary.

4. **Collect the month's weekly summaries** at
   `logs/<year>/<month>/summary_<year>-W<ISO>.md` for weeks whose Monday
   falls in this month, if any exist. These are optional inputs that can
   help identify themes faster, but every claim in the final output must
   still be traceable to a final daily entry, not just the weekly summary.

5. **Determine the destination path**:
   `logs/<year>/<month>/summary_<year>-<month>.md`.

6. **Check for an existing summary** at that path. If one already exists,
   stop and ask before overwriting.

7. **Read each collected final entry in full** (frontmatter + all
   sections), plus any weekly summaries collected in step 4.

8. **Build the summary**, applying `docs/summary-rules.md`:
   - Frontmatter: `date: YYYY-MM`, `status: monthly`, `source_logs` listing
     every final path used.
   - `## Overview` — 1-3 paragraphs: the month in brief.
   - `## By the numbers` — days logged (out of days in month), top tags
     with counts, average mood/energy if consistently recorded across the
     logs used.
   - `## Monthly themes` — 2-4 themes with supporting evidence from final
     logs (quotes or references like `2026-08-15.md#learnings`).
   - `## Key learnings` — synthesized learnings, deduplicated across the
     month's entries/weeks.
   - `## Blockers & carried items` — still-open blockers and rolling
     to-dos still unresolved at month end.
   - `## Next month focus` — `- [ ]` items.
   - Cite sources inline as `YYYY-MM-DD.md` or `YYYY-MM-DD.md#section`.
   - Never introduce a fact absent from the final logs used.

9. **Write the summary file** to the destination path from step 5.

10. **Do not commit or push.** Only do so if the user explicitly asks, per
    `AGENTS.md`.

## Output

Report the month summarized, how many final entries were used as sources
(and which days, if any, had no final entry), and where the summary file
was written.
