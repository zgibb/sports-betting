# CHANGES.md — fork vs. stock

Fork of [georgedouzas/sports-betting](https://github.com/georgedouzas/sports-betting). Stock = `upstream/main`.
Work happens on `zack/main`. Anything that is clearly ours (odds sources, glue, paper-bet log) lives in the separate
`sports-engine` repo, not here.

## Changes vs. stock

None yet. Only `CHANGES.md` and `CLAUDE.md` were added.

## Guardrail

Never install or enable the `execution` extra (`pip install sports-betting[execution]`). It places real bets and
drives bookmaker sites. This engine is paper-only.

## Pulling upstream updates

The `upstream` remote has its push URL set to `DISABLED`, so a push to it cannot happen by accident.

```bash
git fetch upstream --tags
git switch zack/main
git rebase upstream/main          # or: git merge upstream/main
```

The package version comes from git tags (`tool.pdm.version source = "scm"`), so keep upstream tags fetched.
The editable install uses the `pdm-backend` build backend; PDM itself is not needed to install it with uv.

## Known upstream problems (not patched here; worked around in `sports-engine`)

- `NBAStats` requests ESPN date ranges (`dates=YYYYMMDD-YYYYMMDD`), which ESPN now rejects with HTTP 400 (seen
  2026-11-07, upstream 0.15.1). Month form `dates=YYYYMM` works. Workaround: `sports_engine.sources.nba_stats`.
- `resolve_odds` pairs odds to matches on league, division, year, home and away team and ignores the date. For
  sports where a pair meets more than once a season (NBA, NFL playoffs) it can attach odds to the wrong game. Workaround:
  give the odds source the same `name` as the stats source so `DataLoader` skips it, and align by kickoff.
- `NBAStats` keeps ESPN's `TBD vs TBD` placeholder games (NBA Cup knockout slots, seen 2026-11-08 for the 2026-27 season,
  72 rows). They are identical rows, so `check_snapshot_unique` fails and the whole season will not load. Workaround:
  `sports_engine.sources.nba_stats.NBAStatsMonthly` drops them and counts them.
