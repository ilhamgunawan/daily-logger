# Summary Rules (Weekly / Monthly / Annual)

Summaries are derived **only from final daily entries**
(`logs/<year>/<month>/<YYYY-MM-DD>.md`), never from drafts.

## File naming and location

| Kind    | Path                                            | Example                       |
| ------- | ----------------------------------------------- | ----------------------------- |
| Weekly  | `logs/<year>/<month>/summary_<year>-W<ISO>.md`  | `logs/2026/08/summary_2026-W33.md` |
| Monthly | `logs/<year>/<month>/summary_<year>-<month>.md` | `logs/2026/08/summary_2026-08.md`  |
| Annual  | `logs/<year>/summary_<year>.md`                 | `logs/2026/summary_2026.md`   |

### Week boundary rule

- Weeks follow ISO 8601: Monday-Sunday, week number = ISO week
  (`2026-W33`).
- A weekly summary lives in the month folder that contains the week's
  Monday. A week straddling two months accounts for the final logs of
  **both** months in its content, but is only stored once.

## Frontmatter

Weekly: `date` = `YYYY-MM-DD..YYYY-MM-DD` (Monday..Sunday), `status:
weekly`, `source_logs` lists the final paths summarized.
Monthly: `date` = `YYYY-MM`, `status: monthly`.
Annual: `date` = `YYYY`, `status: annual`.

## Weekly summary structure

1. `## Overview` — 1-2 paragraphs: theme of the week, overall tone.
2. `## Highlights` — day-by-day: `2026-08-15 (Sat): <2-3 bullets>`.
3. `## Trends` — recurring topics observed across the week (work, energy,
   mood), each with evidence tag.
4. `## Blockers` — carried blockers, with resolution status if any.
5. `## Next week focus` — 2-5 concrete `- [ ]` items.

## Monthly summary structure

1. `## Overview` — 1-3 paragraphs: month in brief.
2. `## By the numbers` — days logged, top tags (with weekly counts),
   average mood/energy if consistently recorded.
3. `## Monthly themes` — 2-4 themes with supporting evidence from final
   logs (quotes or references like `2026-08-15.md#learnings`).
4. `## Key learnings` — synthesized learnings, deduplicated across weeks.
5. `## Blockers & carried items` — still-open blockers and rolling to-dos.
6. `## Next month focus` — `- [ ]` items.

## Annual summary structure

1. `## Year in brief` — 2-4 paragraphs.
2. `## Monthly timeline` — one line per month with the month's top 1-3
   events/highlights.
3. `## Milestones` — significant achievements with month references.
4. `## Themes of the year` — 3-5 yearly themes.
5. `## Year ahead` — outlook items for the new year.

## General rules

- Cite sources as `YYYY-MM-DD.md` or `YYYY-MM-DD.md#section` inline.
- Never introduce facts absent from the final logs.
- A weekly summary must not be created until its week has ended.