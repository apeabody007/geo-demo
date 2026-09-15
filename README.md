# GEO: The Kalshi Weather Bot

> **Live demo:** **[apeabody007.github.io/geo-demo](https://apeabody007.github.io/geo-demo/)**

An algorithmic trading system for [Kalshi](https://kalshi.com) weather
prediction markets, a CFTC-regulated event-prediction exchange. GEO scans
1°-wide bracket and tail-cutoff contracts on daily-high temperatures across
20 U.S. cities, prices each market against a multi-model probabilistic
forecast, and trades mispricings with real capital.

![GEO operations dashboard, synthetic data](dashboard.png)

---

## What you're looking at

This repository hosts a **public, read-only preview** of GEO's live
operations dashboard, rendered with **fully synthetic data**. No real
positions, no real bankroll, no live API calls. The preview mirrors the
live dashboard section for section: watch list, open positions, resting
orders, P&L and calibration charts, per-cell model drift, skip activity,
the structural-arb detector, and the roadmap. Forecast models appear
under generic labels (Model A through H), and the strategy's parameters
(blend weights, edge thresholds, price filters, sizing constants) are
not encoded anywhere in the page or its data. Source code is private.

The real system runs on the operator's machine against real Kalshi
markets, served as a Tailscale-private PWA.

## What's here

```
index.html              the rendered dashboard (single self-contained file)
manifest.json           PWA manifest
icon-*.png              app icons
```

That's the entirety of the public surface. The dashboard's renderer, data
feed, server, strategy code, calibration models, and trade ledger are all
private and not part of this repository.

## Engineering at a glance

- **Stack:** Python 3.11, signed REST client against the exchange's API,
  SQLite trade ledger, server-rendered vanilla-JS dashboard, Tailscale-served
  PWA.
- **Forecasting:** multi-model probabilistic ensemble with per-station
  bias correction calibrated against historical climate observations.
- **Trading layer:** fractional-Kelly position sizing under multiple risk
  caps; maker-only pricing to sidestep taker fees.
- **Reliability:** single-instance file lock prevents order collisions,
  circuit breaker around upstream APIs throttles rate-limits, year-round
  local-time handling avoids DST settlement misalignment, 600+ pytest
  cases gate every release.
- **Observability:** server-rendered HTML on every page load (no caching
  between operator and the truth), per-cell drift detection, full P&L
  attribution by multiple decision dimensions, calibration reliability
  curve, automated reconciliation against the exchange's official
  settlement source.

## See also

**[Quant Toolkit](https://github.com/apeabody007/Quant-toolkit)**, a
venue-agnostic Claude plugin distilled from operating GEO. Nine skills
covering the full loop from idea to live trading: Kelly sizing,
calibration audit, EMOS bias correction, backtest harness, maker pricing,
P&L attribution, pre-flight checklist, market scanner, drawdown monitor.
Bring your own model and exchange.

## Built by

[Aaron Peabody](https://aaronpeabody.dev). BA Economics (Wisconsin),
BS Psychology (UCF).

