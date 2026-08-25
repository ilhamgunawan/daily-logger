# Standard Daily Log Format

Every enhanced daily entry follows this structure. See `examples/2026-08-15.md` for a complete reference.

## File naming and location

- Final daily entry: `logs/<year>/<month>/<YYYY-MM-DD>.md`
- Draft: `logs/<year>/<month>/drafts/draft_<YYYY-MM-DD>.md`
- Example: `logs/2026/08/2026-08-15.md` and `logs/2026/08/drafts/draft_2026-08-15.md`

## Frontmatter

Required fields:

| Field            | Type         | Notes                                          |
| ---------------- | ------------ | ---------------------------------------------- |
| `date`           | `YYYY-MM-DD` | Log date                                       |
| `weekday`        | string       | English weekday, e.g. `Saturday`               |
| `status`         | `final`      | Always `final` for daily entries               |
| `tags`           | list         | 2-6 lowercase comma-separated keywords         |
| `mood`           | int 1-5      | Self-rated from draft; omit if not in draft    |
| `energy`         | int 1-5      | Self-rated; omit if not in draft               |
| `generated_from` | path         | Relative path to draft, e.g. `drafts/draft_2026-08-15.md` |

For summaries the fields are `date` (range or year), `status` (`weekly`/`monthly`/`annual`), and `source_logs` (list of final log paths used).

## Body sections

### 1. `## Summary` (required)

1-3 paragraphs distilling the day: emphasis, themes, and outcome.
No bullet points here.

### 2. `## Accomplishments` (required)

Bullet list of completed work/tasks. One bullet per item, past tense,
start with a verb. Order by impact, not chronology.

### 3. `## Learnings` (required if any)

One bullet per learning, each ending with a bolded 1-line takeaway:
`**Takeaway:** ...`

### 4. `## Blockers / Next steps` (required if any)

`- [ ]` items for next steps, `**Blocked:**` prefix for blockers with the
reason attached. Omit the section entirely if neither applies.

### 5. `## Day in detail` (required)

STAR blocks for each major activity, most significant first. Each block:

#### Activity: <short name> (`<time range or 0h30m>`)

- **Situation:** context that led to this activity
- **Task:** the goal or problem to address
- **Action:** what was actually done (concrete, factual)
- **Result:** measurable or observable outcome
- **Reflection:** what worked, what to change next time

Minor activities from the draft (small tasks, errands) may be folded into
`Accomplishments` instead of getting their own STAR block.