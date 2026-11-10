# LOG: <property>

Append only. One line per action, newest at the bottom. Start failure lines with `FAIL:` so the scorecard can count them.

Line shapes:

- `<date time TZ>: read MISTAKES.md, BRIEF, STATE, last 3 LOG lines`
- `<date time TZ>: PICK <one change>; parked: <option 2>, <option 3>`
- `REVIEW PR#<n> <PASS|FAIL> items: <numbers> preview: <url>`
- `<date time TZ>: OWNER YES PR#<n> at <full head SHA>`
- `<date time TZ>: MERGED PR#<n> <merge SHA>, deploy <id>`
- `<date time TZ>: LIVE <url> curl 200, found "<exact string>"`
- `FAIL: <date time TZ> <what did not run or what broke>`
