# HSA Trackr: a programmatic SEO site run by an agent team

[HSA Trackr](https://www.hsatrackr.com) is my consumer site for people with a health savings account: provider comparisons, fee pages, calculators, eligibility tools and receipt tracking. Most of its pages are generated from structured data, and an agent team runs its SEO every week.

## The shape of the site

- About 2,600 URLs in the sitemap, most of them programmatic: provider comparisons, alternatives, calculators, state pages and FAQs, each built from a JSON record.
- A freeze check in the build verifies every programmatic record (2,737 at the last run) and a fact scan blocks known-bad claims before deploy.
- 311 pages carry protected prose with a hashed baseline, so a change to that copy shows up in a test.
- The conversion is free signup. A paid founding plan is second. Rankings are a means, not the score.

## The team

| Role | Seat | Job |
|---|---|---|
| Lead | the lead seat | Picks the week's change, runs review, brings me the PR |
| Researcher / operator | HSA SEO | Search Console and live-page evidence, live verify after deploy |
| Writer | Voice (site mode) | Page copy from the evidence file only, then human-copy |
| Builder | Cursor cloud agent, or a coding seat for big jobs | One draft PR from a prompt file |

## What one week looks like

The Monday routine reads the mistakes file, the brief, the state file and the last log lines. The researcher pulls 28 days of Search Console data. If the data source is offline, the run writes a loud FAIL line instead of reusing old data. The lead and the researcher pick one change, the researcher checks it four ways (the live page, the search results page, AI answers and the conversion path), the writer drafts, and a builder opens a draft PR. The lead runs the checklist against the preview deploy. I get the PR link, the review line and a plain list of what changes. After my yes, it merges, deploys and gets a curl receipt from production.

## Example: the thin calculator pages (October 2026)

- **What the researcher found (2026-10-08):** 71 of the 73 `/calculator/*` URLs in the sitemap rendered a wrapper that listed input labels as text and computed nothing. That is thin content on a site that depends on trust.
- **The plan, split into five small PRs:**
  - 301 the pages that had a real tool or a same-topic page to go to.
  - Noindex 18 more.
  - Build real tools for the rest, starting with the excess-contribution penalty and investment growth families.
- **Builder briefs:** each PR had its own prompt file listing the files it could edit. The prompt also listed the files that belonged to the other open PRs.
- **What review caught:** two of the PRs would break each other's sitemap-count test depending on merge order. The lead wrote a merge-order note with the fix that had to land on whichever PR merged second.
- **The yes:** I approved the redirect PR on 2026-10-09 at its exact head commit, with 38 redirects. The yes carried over only if the rebase onto the new main was clean.

## What I took from it

- Programmatic SEO scales mistakes as fast as pages. The useful automation here is the gate, not the generator.
- Small PRs with written file scopes let several agents work on one repo on the same day without stepping on each other.
- "Live" means a curl of production, not a merged PR.

## Not shown

Traffic numbers, signups, partner terms and the repo itself stay private. The public spin-off from this build is [emdash-hsa-limits](https://github.com/mavericksolutions7/emdash-hsa-limits), a sourced IRS limits plugin.
