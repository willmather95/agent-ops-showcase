# Failure checklist: <team>

## Ship gate

Every merge or deploy needs the owner's explicit yes on that PR, after this checklist passes and the REVIEW line is written. A yes covers one PR at one head commit. A new commit needs a new yes. No reply means hold.

## Part 1: top failures per seat

| Seat | Failure | How we notice | What happens next |
|---|---|---|---|
| Lead | Ships two changes in one week | Scorecard shows 2+ merged changes in one week | Next change waits a full week |
| Lead | Merges without a PASS line or an owner yes | LOG has a merge SHA with no REVIEW PASS or OWNER YES above it | Tell the owner the same day; offer a revert PR; add a MISTAKES line |
| Researcher | Data source offline | Export script cannot run | LOUD FAIL in LOG; the week doc names the last real export |
| Researcher | A number goes on a page without a source | Reviewer finds no URL and check date for it | Review FAIL; the number comes out |
| Writer | AI tells or em dashes in public copy | Checklist item 6 grep | Back to the writer |
| Builder | PR touches files outside the prompt's scope | PR file list vs the prompt | Review FAIL; narrow the PR or relaunch |
| Builder | CI red | Check runs on the PR | One fix attempt, then stop and report |

## Part 2: pre-merge checklist

Run against the preview URL. Write one line to LOG: `REVIEW PR#<n> <PASS|FAIL> items: <numbers> preview: <url>`

| # | Check | Pass |
|---|---|---|
| 1 | Every new or changed claim maps to a source URL in the evidence folder | 100% mapped |
| 2 | Every price or fee shows a check date | All dated, none older than 35 days |
| 3 | Every new or changed link returns 200 after redirects | All 200 |
| 4 | Brand spelling | No misspellings of our brand |
| 5 | Title and meta | One brand suffix; meta under about 160 characters and true |
| 6 | Human-copy pass | Flag list exists; zero em dashes and kill-list words |
| 7 | Mobile screenshot at 390x844 | No overlap; call to action visible |
| 8 | Call to action | Goes to the right page and returns 200 |
| 9 | Tests | CI green, including any protected-copy baseline |
| 10 | Scope | Only the files named in the builder prompt changed |
