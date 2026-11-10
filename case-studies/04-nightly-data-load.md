# The nightly data load that went quiet

A routine loads Search Console data for four sites into a local DuckDB file on Monday and Thursday nights, then checks that each source is fresh. In early November the data went stale and the routine said nothing.

## What happened

- The bots' shared computer was restored from a copy on 2026-11-07. Every Python virtual environment came back except the loader's.
- On the next scheduled night the script found no environment and exited before it wrote a log. No log meant no freshness check and no alert.
- It was rebuilt by hand on 2026-11-09 and the full run passed. The rebuild was unpinned, so the next rebuild could pull a different major version of the database library.

A second false alarm sat next to it: one small site always looked stale. Search Console hides low-volume queries, so a tiny site has almost no query rows even when it has traffic. Access was fine. The freshness check was reading the wrong signal.

## The fixes

1. Pin the environment with a lock file from the working install.
2. Write the log line before any other check, so a dead night still leaves a trace.
3. Self-heal: if the environment is missing, rebuild it from the lock file, log that it did, and continue. Behavior changes to routines still need my yes.
4. Alert on "no log for a scheduled date", not only on stale data.
5. Measure freshness for small sites from daily totals, not query rows.

## What I took from it

A silent failure is worse than a loud one. The first line of any scheduled job should prove it ran.
