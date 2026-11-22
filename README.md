# SwiftSite

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/stevewhy404/site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/stevewhy404/site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

**SwiftSite** is a faster drop-in replacement for make.fun's own
[makefun-site 1.0.0](https://make.fun/bounty/site-generator-speed-01-run-20261122),
built for make.fun's
[$100 "Build a static site faster, 22 November 2026" bounty](https://make.fun/bounty/site-generator-speed-01-run-20261122).

It answers exactly as makefun-site 1.0.0 does on every case — same output
tree, byte for byte — but with less CPU time. Places go by CPU time, least
first, and an entry only qualifies for a reward by beating the house
baseline at 95% confidence.

## How it works

`main.ts` is the program the harness runs: it reads every case from
`/input/cases.json`, answers each one with `run()` from `solve.js`, and
writes `/output/answers.json`. `solve.js` is a dependency-free ES module
that re-implements makefun-site's build — its own front matter, template
dialect, Markdown subset, slug rule and build report — with the hot paths
rewritten for speed: single-pass parsing, no repeated work across the
200–600 sources of a case, and no per-page re-rendering of shared data.

## Benchmark

On the kit's practice set, SwiftSite produces byte-identical answers to
the house baseline (official scorer: `passed: 1, cases_passed: 3/3`) and
runs measurably faster. CPU time of `run()` on the practice set (3 cases,
fresh process, `process.cpuUsage`, 3 runs each, this VM):

| | run CPU time |
|---|---|
| makefun-site 1.0.0 (house baseline) | ~868–919 ms (avg ~889) |
| SwiftSite | ~491–532 ms (avg ~506) |

Speedup ≈ **1.76x** on compute; whole-program wall time ≈ 600 ms vs
≈ 1.050 ms for the baseline. Two executions produce byte-identical
`answers.json`. Repo size 36.860 bytes (limit 4 MiB).

## License

MIT — see [LICENSE](LICENSE).
