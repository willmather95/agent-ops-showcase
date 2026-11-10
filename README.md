# agent-ops-showcase

How I run a fleet of AI agents on my own businesses: who does what, how work moves between them, and what stops a bad change from reaching a live site.

This is the operating model, not the vault. Prompts, logs, customer data and business numbers stay private. Everything here is either a sanitized copy of a real file or a description of something that ran, with the date it happened. [NOTES.md](NOTES.md) lists where each fact comes from.

## The setup in one paragraph

About two dozen Grok Bot seats, each with one job, plus Cursor cloud agents and Claude Code or Codex sessions for code. One lead seat hands out work and runs the review gate. Researchers bring evidence with a source for every number. A writer turns evidence into copy and runs a de-AI pass. Builders open small pull requests from a prompt file. Nothing merges or deploys until I say yes to that pull request at that commit. Scheduled routines do the repeat work, and two healthcheck routines watch the routines.

## Read this first

| | |
|---|---|
| [Architecture](docs/architecture.md) | Seats, handoff files, the ship gate, review loops and routines, with a diagram |
| [Case study: HSA Trackr weekly SEO loop](case-studies/01-hsa-trackr-weekly-loop.md) | A programmatic SEO site run by a four-role agent team, one verified change a week |
| [Case study: the bot that skipped review](case-studies/02-the-bot-that-skipped-review.md) | An older automation pushed an unsourced FAQ straight to production. What broke, how it was caught, and the fix |
| [Case study: cutting the fleet down](case-studies/03-seat-consolidation.md) | Going from about 19 seats around one person to two teams with 5 active seats, without deleting anything |
| [Case study: the nightly data load that went quiet](case-studies/04-nightly-data-load.md) | A silent failure in the analytics loader and the three rules it produced |
| [Templates](templates/) | Blank copies of the handoff files every seat reads: BRIEF, STATE, LOG, MISTAKES, the failure checklist and a cloud-agent prompt |

## Public pieces you can run

| Repo | What it is |
|---|---|
| [seo-pack](https://github.com/willmather95/seo-pack) | The SEO skills the weekly loop runs on |
| [agent-ops-skills](https://github.com/willmather95/agent-ops-skills) | Fleet upkeep: routine and transcript healthchecks, overnight watch, coding-seat handoff, page and video QA |
| [vault-memory](https://github.com/willmather95/vault-memory) | Shared Git-backed memory for every bot |
| [human-copy](https://github.com/willmather95/human-copy) | The de-AI writing pass every public sentence goes through |
| [world-class-charts](https://github.com/willmather95/world-class-charts) | React chart and KPI components used in the dashboards |
| [agent-rules-restructure](https://github.com/willmather95/agent-rules-restructure) | Shrinks sprawling CLAUDE.md / AGENTS.md files into one shared root |
| [emdash-hsa-limits](https://github.com/mavericksolutions7/emdash-hsa-limits) | Sourced IRS HSA limits as a CMS plugin, from the HSA Trackr build |

## What I would tell a team deploying agents

1. **Give every agent one job and a written "not allowed" list.** Most failures I have seen came from an agent doing a reasonable thing that was someone else's job.
2. **Make evidence a file, not a claim.** If a number has no URL and check date, it does not go on a page.
3. **Gate on the change, not the agent.** A standing "you may ship" grant lasted one day in my setup. A yes now covers one pull request at one commit.
4. **Put the checks in code where code can do them.** The worst incident here passed because the tests existed but nothing ran them.
5. **Watch the watchers.** Routines drift, go quiet or burn usage. A weekly audit of the routines themselves is cheap.

## Contact

[LinkedIn](https://www.linkedin.com/in/willmather)
