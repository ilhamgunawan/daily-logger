# AGENTS.md

Convention-driven daily activity logger. The agent performs all conversions
following the rules in `docs/` — there is no code, no build, no tests.

## Repo layout

- `logs/<year>/<month>/` — final daily entries `YYYY-MM-DD.md`
- `logs/<year>/<month>/drafts/` — raw drafts `draft_YYYY-MM-DD.md`
- `logs/<year>/<month>/summary_<year>-W<ISO>.md` — weekly summaries (ISO weeks)
- `logs/<year>/<month>/summary_<year>-<month>.md` — monthly summaries
- `logs/<year>/summary_<year>.md` — annual summaries
- `docs/format.md` — standard format spec (frontmatter + sections)
- `docs/enhancement-rules.md` — draft-to-final rules (STAR, no fabrication)
- `docs/summary-rules.md` — weekly/monthly/annual summarization rules
- `examples/` — reference draft/final pair

## Workflows

1. **Enhance draft**: for each `drafts/draft_*.md` without a matching final
   entry, generate `YYYY-MM-DD.md` per `format.md` + `enhancement-rules.md`,
   and delete the processed draft only when asked.
2. **Summarize** (only after the period's final entries exist): weekly
   (Monday-Sunday, ISO week), monthly, annual — per `summary-rules.md`.
3. **Push to GitHub** (asked explicitly): commit and push; never commit on
   your own.

## Skills / commands / agents

The workflows above are implemented as ready-to-invoke prompts for every
supported agent runtime — use them instead of re-deriving the steps
manually:

- Claude Code skills: `.claude/skills/<name>/SKILL.md`, invoked as
  `/<name>` or triggered by intent.
- opencode commands: `.opencode/command/<name>.md`, invoked as `/<name>
  [args]`.
- GitHub Copilot CLI custom agents: `.github/agents/<name>.agent.md`,
  invoked via `/agent`, "use the `<name>` agent", or
  `copilot --agent <name> --prompt "..."`.

All three define the same four workflows, kept in sync:

- `enhance-draft` — draft → final daily entry
- `summarize-week` — final entries → weekly summary
- `summarize-month` — final entries → monthly summary
- `summarize-year` — final entries → annual summary

## Critical rules

- Never invent facts; mark gaps `(needs detail)` (see enhancement rules).
- Summaries derive only from final entries, never drafts.
- Read `docs/` before producing any log file — they are the source of truth.