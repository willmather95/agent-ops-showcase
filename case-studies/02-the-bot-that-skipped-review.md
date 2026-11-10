# The bot that skipped review

On 2026-11-08 an automation pushed an unsourced FAQ about named competitors to a live page on HSA Trackr. The agent team caught it two days later in its weekly review. This is what happened and what changed.

## What it was

This was not one of the fleet's seats. It was a GitHub Actions workflow from May 2026, older than the team setup. Every Sunday it pulled page-two queries from Search Console, asked a hosted model to write an FAQ answer for each one, committed the result with `[skip ci]` and pushed straight to `main`.

## What went wrong, in order

1. **The prompt asked for names without facts.** It told the model to "reference real providers" and gave it no sources. The model wrote comparative and pricing claims about three named providers.
2. **The bar to write was low.** A query with 5 impressions qualified. The question was also reworded on the way in, so the answer drifted from what people searched for.
3. **The workflow could push to main.** It had `contents: write`, and `main` had no protection. Branch protection is not available on a private repo on a free personal plan.
4. **The tests existed but nothing ran them.** A protected-prose test broke on this commit. No workflow ran the test suite on push, and the build script ran fact and freeze checks but not that test. `[skip ci]` skipped nothing that tested anything, and the host deployed anyway.
5. **The red run looked like "nothing shipped".** The run failed at its last step, a stats printout after the push. A red run still shipped.

## How it was caught

The researcher seat flagged it as defect D1 in its weekly review on 2026-11-10. It found a page claim with no source behind it. The lead then traced the commit, the workflow, the prompt, the missing CI and the live page, and wrote a fix plan. Nothing was reverted or changed without my yes.

## The fix: free, no paid plan

Branch protection on a private personal repo needs a paid GitHub plan. I said no to that and used three free gates in its place:

1. **The bot works like every other builder.** The workflow writes to a dated `bot/` branch and opens a draft PR. It no longer pushes to `main`. Its token is limited to what that needs: write the branch and open the PR.
2. **CI on every PR.** A test workflow runs the full suite and the protected-prose check on every pull request and every push to `main`.
3. **The deploy refuses drift.** The protected-prose check also runs in the build. If copy changes without a matching baseline update, the production build fails, even if something reaches `main`.

Around those gates:

| # | Change | Why |
|---|---|---|
| 1 | Disable the workflow before its next Sunday run | Stop new writes first |
| 2 | One-file PR removing the FAQ, keeping the data reports | Undo only the bad part |
| 3 | A citation gate: every generated answer carries a source URL and a quote that is checked live; no named-provider pricing or superlatives without one | Fix the root cause in the prompt |
| 4 | Fix the stats crash | A red run should mean something |

Every one of these goes through the same per-PR yes as the rest of the fleet. As of 2026-11-10 they are planned and in progress, not done.

What this does not do: on a free private repo, nothing in GitHub hard-blocks a direct push to `main` by someone with write access. The gates make a bad change fail CI and fail the build, and the bot no longer has a reason to push there. I judged that enough for a one-person business. At a company I would pay for the hard block.

## What I took from it

- The gate has to cover every writer, including the old cron job nobody thinks of as an agent.
- Tests that exist but don't run give you false confidence. Wire them into the path to production.
- Ask a model for named facts without giving it sources and it will make them up. Ask for a quote you can check instead.
