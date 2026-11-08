# CLAUDE.md

Fork of georgedouzas/sports-betting (`zgibb/sports-betting`), used as the modeling and backtesting library for the
sports engine in `..\sports-engine`. Read `..\..\..\README.md` (trading-hub rules) and `..\PROMPT.md` first.

## Rules here

- Paper only. **Never install or enable the `execution` extra**: no bookmaker credentials, no automating bookmaker sites.
- Keep fork edits minimal and listed in `CHANGES.md`. Our own code goes in `..\sports-engine`.
- Work on branch `zack/main`. Never push to `upstream` (its push URL is `DISABLED`).
- Python >=3.11,<3.14. Package source is in `src\sportsbet`. Version comes from git tags (scm).

## Useful facts

- Stats sources: `NBAStats` (ESPN, free), `EuroLeagueStats`, football-data soccer. No NFL or college football source.
- Odds sources live in `src\sportsbet\sources\_odds`; follow that pattern for new ones (our OddsHarvester source goes in
  `sports-engine`).
- Dataloader: `sportsbet.dataloaders.DataLoader(param_grid=..., stats=..., odds=...)`.
