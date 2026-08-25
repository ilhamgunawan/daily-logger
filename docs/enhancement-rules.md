# Enhancement Rules (Draft -> Final)

Rules for converting a draft at `logs/<year>/<month>/drafts/draft_YYYY-MM-DD.md`
into the standard final entry at `logs/<year>/<month>/YYYY-MM-DD.md`.

## Hard rules

1. **Never fabricate.** All facts, numbers, and claims come from the draft.
   If a draft detail is ambiguous or missing, keep it vague or mark it
   `(needs detail)` — never invent content.
2. **Preserve everything meaningful.** No fact from the draft may be
   silently dropped. Merge duplicates, but keep the information.
3. **Self-contained.** The final must be readable without the draft: no
   "as I mentioned", no dangling references.
4. **Stick to the template.** Sections per `docs/format.md`, in order.
   Empty required sections get `_None._`; optional sections are omitted.
5. **One pass.** Do not rewrite an already-final file unless explicitly asked.

## Structure rules

- Group draft notes into categories first: work, learning, personal,
  health, social, errands — only if > 1 note per category.
- Order activities in `Day in detail` by significance, then chronology.
- A major activity (≥ 30 min focus, or notable outcome) gets a STAR block.
  Quick tasks go into `Accomplishments` bullets.

## Style rules

- First person, past tense, plain factual language. No marketing tone.
- Bullets: start with a verb, keep under ~20 words where possible.
- Preserve the draft's own voice and level of detail; never inflate
  ("fixed one failing test" stays that, it does not become "overhauled
  the test infrastructure").
- Timestamps from the draft are preserved (`09:00-10:30`, `0h45m`).

## STAR expansion guidance

For each STAR block:

- **Situation**: 1 line — what was happening before.
- **Task**: 1 line — the concrete goal/problem.
- **Action**: 2-5 lines — concrete steps actually taken.
- **Result**: 1-3 lines — observable outcome; numbers when available.
- **Reflection**: 1-2 lines — what worked / what to change next time;
  omit this element if the draft gives no basis for it.

If the draft describes the activity flat ("worked on X"), expand only to the
detail the draft supports; when expansion is required for readability, write
inferences as questions in `Reflection` or mark `(needs detail)`, never as
invented facts.