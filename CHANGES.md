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
