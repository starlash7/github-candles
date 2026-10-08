# RULES.md - github-candles Working Rules

These rules apply to the whole repository, for humans and coding agents alike.

## Workflow

- One workspace and one branch per task. Do not rename an existing branch
  unless the user requests it.
- Read `generate_chart.py` and `.github/workflows/chart.yml` before changing
  chart behavior.
- Record material decisions in `decisions/` (see `decisions/README.md`).
- Report commands and actual results. An unrun check remains unverified.
- Open a PR against `main`; merge only after the PR check passes.

## Data Honesty

- The GitHub contributions API returns one total per day. True intraday OHLC
  does not exist.
- Candles use `open = previous period total`, `close = current period total`,
  `high = max(open, close)`, `low = min(open, close)`.
- Never synthesize wicks, intraday highs/lows, or any value not derived from
  real contribution counts. Derived indicators (e.g. moving averages) are fine.
- Mock data is only for local runs and CI checks without a token. Never commit
  a mock-generated chart.

## Code

- Python stdlib only. Do not add dependencies.
- Keep `generate_chart.py` a single, copy-pasteable file.
- Adding a mode must not change the output of existing modes.
- Prefer the smallest code that solves the request. Use clear verb+noun names.
- Do not edit files outside the requested scope.

## Design

- Exchange-style dark UI using the palette constants in `generate_chart.py`.
- New colors must sit with the existing palette and stay legible on `BG`.
- Check each changed SVG visually before opening a PR.

## Verification

- `python generate_chart.py` for every mode (`year`, `month`, `daily`) must
  succeed and produce well-formed SVG.
- The `check` workflow runs the same on every PR.
