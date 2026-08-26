---
description: Generate an annual summary from a year's finalized daily entries, following this repo's summary rules.
agent: build
---
Produce one annual summary from a year's finalized daily logs. This
implements the annual part of the "Summarize" workflow described in
`AGENTS.md` and `README.md`.

Target year: $ARGUMENTS
(`YYYY`, or "this year"/"last year". If ambiguous, ask which year to
summarize rather than guessing.)

Steps:

1. **Read the rules first.** Load `docs/summary-rules.md` in full — it
   defines file naming, frontmatter, and the annual section structure.

2. **Check the year has ended.** An annual summary should reflect a
   complete year. If the target year is the current, still-in-progress
   year, stop and confirm before proceeding (the user may explicitly want
   a partial-year summary).

3. **Collect the year's final entries.** Look for every
   `logs/<year>/<month>/YYYY-MM-DD.md` across all twelve months. Use
   **only** final entries — never drafts. If **no** final entries exist for
   the year, stop and report that instead of producing an empty summary.

4. **Collect the year's monthly summaries** at
   `logs/<year>/<month>/summary_<year>-<month>.md` for any months that have
   one, and its weekly summaries at
   `logs/<year>/<month>/summary_<year>-W<ISO>.md` where useful. These are
   optional inputs that speed up finding themes and milestones, but every
   claim in the final output must still be traceable to a final daily
   entry, not just a monthly/weekly summary.

5. **Determine the destination path**: `logs/<year>/summary_<year>.md`.

6. **Check for an existing summary** at that path. If one already exists,
   stop and ask before overwriting.

7. **Read the collected sources**: every final entry, plus any monthly and
   weekly summaries gathered in step 4.

8. **Build the summary**, applying `docs/summary-rules.md`:
   - Frontmatter: `date: YYYY`, `status: annual`, `source_logs` listing
     every final path used.
   - `## Year in brief` — 2-4 paragraphs.
   - `## Monthly timeline` — one line per month with that month's top 1-3
     events/highlights (omit months with no final entries, or note them as
     unlogged).
   - `## Milestones` — significant achievements with month references.
   - `## Themes of the year` — 3-5 yearly themes, each with supporting
     evidence.
   - `## Year ahead` — outlook items for the new year.
   - Cite sources inline as `YYYY-MM-DD.md` or `YYYY-MM-DD.md#section`.
   - Never introduce a fact absent from the final logs used.

9. **Write the summary file** to the destination path from step 5.

10. **Do not commit or push.** Only do so if explicitly asked, per
    `AGENTS.md`.

Report the year summarized, how many final entries were used as sources
(and which months, if any, had no final entries), and where the summary
file was written.
