# Builder prompt: <PR name> (draft PR only)

Written <date> by <seat> for <lead> to launch. Plan: `<path to the plan>`. Evidence: `<path>`.

## Ground rules

- Repo: `<owner/repo>`. Base: latest `main` (was `<sha>` on <date>; pull first).
- Branch: `<branch name>`
- Open as a **draft PR**. Do not merge, deploy, mark ready for review, or ask the owner for approval.
- Brand is always **<exact spelling>**.
- No em dashes in anything human-readable you add (PR body, comments, copy).

## Goal

<One paragraph: what is wrong today, with the evidence, and what the PR changes.>

## Files you may edit

1. `<path>`
2. `<path>`
3. Tests: `<path>`

Anything else: stop and report instead.

## Files you must not touch (other open work)

- PR #<n> (head `<sha>`): `<paths>`
- Branch `<name>`: `<paths>`

## Done when

- `<test command>` passes, including `<baseline or guard test>`.
- The preview deploy shows `<exact string or behavior>`.
- The PR body lists every file changed and links this prompt.
