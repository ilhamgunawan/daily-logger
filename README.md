# Daily Logger

Convention-driven daily activity logger — a small repository of rules and workflows for converting raw drafts into finalized daily logs, and producing weekly/monthly/annual summaries.

This repository is primarily authored for an automated agent to operate against the files using the rules in `docs/`. The agent that typically interacts with this repo is an AI assistant using the Copilot CLI runtime in VS Code.

Table of Contents
- [About](#about)
- [How to use](#how-to-use)
- [Repo layout](#repo-layout)
- [Workflows](#workflows)
- [Critical rules](#critical-rules)
- [How to use (manual steps)](#how-to-use-manual-steps)
- [Examples](#examples)
- [Contributing](#contributing)
- [License](#license)

About
-----
Daily Logger stores daily notes as markdown files following a small set of content and enhancement rules. The repo separates raw draft entries from final entries and provides rules for summarization. The authoritative specification for formats and enhancement rules lives in the `docs/` folder — read those before creating or modifying log files.

How to use
----------
Since your logs may contain personal or private information, run your own private copy rather than committing directly to this repo:

1. Fork this repo.
2. Set the forked repo to **private** — this prevents personal information in your logs from being publicly leaked.
3. Clone your forked repo to your local machine.
4. Start using it: drop raw notes into `logs/<year>/<month>/drafts/draft_YYYY-MM-DD.md` and let your agent (or you, manually) enhance and summarize them following the rules in `docs/` and `AGENTS.md`.

Repo layout
-----------
- [AGENTS.md](/Users/ilham/Projects/daily-logger/AGENTS.md) — agent conventions and the main agent workflows.
- [docs/](/Users/ilham/Projects/daily-logger/docs/) — format and rules the agent must follow (see `format.md`, `enhancement-rules.md`, `summary-rules.md`).
- [logs/](/Users/ilham/Projects/daily-logger/logs/) — generated final logs and drafts; structure below:
  - `logs/<year>/<month>/` — final daily entries `YYYY-MM-DD.md`
  - `logs/<year>/<month>/drafts/` — raw drafts `draft_YYYY-MM-DD.md`
  - `logs/<year>/<month>/summary_<year>-W<ISO>.md` — weekly summaries (ISO weeks)
  - `logs/<year>/<month>/summary_<year>-<month>.md` — monthly summaries
  - `logs/<year>/summary_<year>.md` — annual summaries
- [examples/](/Users/ilham/Projects/daily-logger/examples/) — reference draft/final pairs (if present)

Workflows
---------
1. Enhance draft
   - For each `logs/<year>/<month>/drafts/draft_*.md` that does not yet have a matching final entry, produce `logs/<year>/<month>/YYYY-MM-DD.md` that conforms to `docs/format.md` and `docs/enhancement-rules.md`.
   - Do not delete the draft automatically. Delete only when explicitly requested.

2. Summarize
   - When all final entries for the period exist, produce summaries derived only from the final entries:
     - Weekly (Monday–Sunday, ISO week) — `summary_<year>-W<ISO>.md`
     - Monthly — `summary_<year>-<month>.md`
     - Annual — `summary_<year>.md`
   - Summaries must follow the rules in `docs/summary-rules.md` and must not invent facts.

3. Push to GitHub
   - Only performed when explicitly requested by a human. The agent must never push changes on its own.

Critical rules
--------------
- Never invent facts. If a draft lacks information, mark gaps with `(needs detail)` as described in `docs/enhancement-rules.md`.
- Summaries must be generated only from final entries; drafts are not sources for summarization.
- Read the `docs/` files before producing or modifying any log or summary file — they are the single source of truth.

How to use (manual steps)
-------------------------
These are simple manual steps for contributors or for validating what the agent does:

1. Read the rules
   - Open [docs/format.md](/Users/ilham/Projects/daily-logger/docs/format.md) and [docs/enhancement-rules.md](/Users/ilham/Projects/daily-logger/docs/enhancement-rules.md).

2. Inspect drafts
   - Check `logs/<year>/<month>/drafts/` for `draft_YYYY-MM-DD.md` files.

3. Produce a final entry
   - Using the format in `docs/format.md`, create `logs/<year>/<month>/YYYY-MM-DD.md`. If required details are missing, include `(needs detail)` placeholders.

4. Create summaries
   - After all final entries for a week/month/year are present, create the corresponding summary files per `docs/summary-rules.md`.

5. Commit & push
   - Only commit and push changes when explicitly asked. If performing commits, follow the repository's commit message policy and include a Co-authored-by trailer for agent-assisted commits if applicable.

Examples
--------
See the [examples/](/Users/ilham/Projects/daily-logger/examples/) directory for sample draft/final pairs and example summaries. Use them as references when creating new entries.

Contributing
------------
- Changes to the rules in `docs/` should be discussed and reviewed before being applied because they affect the agent's behavior.
- For content contributions (new logs, edits to final entries), open a PR describing the intent. Do not rely on the agent to push changes without explicit instruction.

License
-------
Code: GNU General Public License v3.0 or later (GPL-3.0-or-later). See [LICENSE](/Users/ilham/Projects/daily-logger/LICENSE).

Content (logs, docs, examples): Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0). See [LICENSE-CONTENT](/Users/ilham/Projects/daily-logger/LICENSE-CONTENT).

Note: Personal or private log entries in `logs/` may include sensitive information — verify the intended distribution before publishing or reusing content from that directory.

Contact
-------
Repository: ilhamgunawan/daily-logger

Acknowledgements
---------------
This repository is designed to be used by an automated agent that follows the conventions in [AGENTS.md](/Users/ilham/Projects/daily-logger/AGENTS.md). The agent acting in this workspace is an AI assistant using the Copilot CLI runtime in VS Code.
