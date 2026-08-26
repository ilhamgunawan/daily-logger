# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A convention-driven daily activity logger. There is no code, no build, no
tests, no dependencies — the entire repo is markdown files plus a set of
rules documents. The "product" of this repository is the agent's disciplined
application of those rules when converting drafts into final logs and
summaries. Always read the relevant `docs/*.md` file before creating or
modifying any log/summary file — they are the single source of truth, not
this file.

## Repo layout

- `docs/format.md` — required frontmatter + body section structure for a final daily entry.
- `docs/enhancement-rules.md` — rules for turning a draft into a final entry (no fabrication, STAR expansion, style).
- `docs/summary-rules.md` — rules for weekly/monthly/annual summaries, including ISO week boundaries and file naming.
- `logs/<year>/<month>/` — final daily entries: `YYYY-MM-DD.md`.
- `logs/<year>/<month>/drafts/` — raw drafts: `draft_YYYY-MM-DD.md`.
- `logs/<year>/<month>/summary_<year>-W<ISO>.md` — weekly summaries.
- `logs/<year>/<month>/summary_<year>-<month>.md` — monthly summaries.
- `logs/<year>/summary_<year>.md` — annual summaries.
- `examples/` — a reference draft/final pair (`draft_2026-08-15.md` → `2026-08-15.md`); use as the template for tone and structure.

## Core workflows

1. **Enhance draft → final**: for each `drafts/draft_YYYY-MM-DD.md` without a
   matching `logs/<year>/<month>/YYYY-MM-DD.md`, generate the final entry per
   `docs/format.md` and `docs/enhancement-rules.md`. Do not delete the draft
   unless explicitly asked.
2. **Summarize**: only after all final entries for a period exist, generate
   weekly (ISO Monday–Sunday), monthly, or annual summaries per
   `docs/summary-rules.md`, derived **only** from final entries — never from
   drafts. A weekly summary must not be created until its week has ended.
3. **Push to GitHub**: only when explicitly requested by the human; never
   commit or push on your own initiative.

## Skills

This repo ships Claude Code project skills under `.claude/skills/` that
implement the core workflows directly — prefer invoking these over
re-deriving the steps manually:

- `enhance-draft` — converts a selected draft into its final daily entry
  (Enhance draft workflow).
- `summarize-week` — generates a weekly summary for a given ISO week.
- `summarize-month` — generates a monthly summary for a given month.
- `summarize-year` — generates an annual summary for a given year.

Each skill's `SKILL.md` embeds the relevant rules from `docs/` (existing-file
checks, source-of-truth constraints, output structure) so following the
skill satisfies the critical rules below.

Equivalent implementations exist for other runtimes, all defining the same
four workflows — keep them in sync when a workflow's rules change:

- opencode commands: `.opencode/command/<name>.md`, invoked as
  `/<name> [args]`.
- GitHub Copilot CLI custom agents: `.github/agents/<name>.agent.md`,
  invoked via `/agent`, "use the `<name>` agent", or
  `copilot --agent <name> --prompt "..."`.

## Critical rules (apply across all workflows)

- **Never fabricate.** Every fact, number, or claim in a final entry or
  summary must trace back to a draft/final log. If information is missing or
  ambiguous, mark it `(needs detail)` rather than inventing it.
- **Preserve everything meaningful** from a draft — merge duplicates, but
  never silently drop a fact.
- **One pass.** Do not rewrite an already-final file unless explicitly asked.
- **Self-contained output.** A final entry must read standalone, with no
  reference back to the draft ("as mentioned above", etc.).
- Follow the template section order exactly; empty required sections get
  `_None._`, optional sections are omitted entirely if not applicable.
- Cite sources in summaries as `YYYY-MM-DD.md` or `YYYY-MM-DD.md#section`.

## Licensing note

Code in this repo (none currently, but tooling/scripts if added) is
GPL-3.0-or-later; content (`logs/`, `docs/`, `examples/`) is
CC BY-SA 4.0. Entries under `logs/` may contain personal/sensitive
information — verify intended distribution before publishing or reusing it.
