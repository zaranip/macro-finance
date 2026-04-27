# AI citations — HW2

We used Claude (Sonnet/Opus) as a coding and writing assistant throughout this assignment. Notes on what we asked for and how we used the output:

## Data sources / NDL switch
We initially used yfinance for ETF and index data. We then asked the AI to migrate the notebook to **NASDAQ Data Link `QUOTEMEDIA/PRICES`** (one of our entitled subscriptions: SPY, HYG, DBC, IEF). The AI adapted the data-fetching layer (`ndl.get_table` with paginated calls and adjusted-close columns) and noted that QUOTEMEDIA's last row is 2025-05-29, so the risk-parity backtest in Q8–Q10 ends there. The AI also flagged that CME fed funds futures are not in our NDL bundle and we therefore continue to use Databento for the single Dec-2027 ZQ quote.

## Q1 — Fed funds market pricing
We asked the AI to suggest a clean way to read end-2027 fed-funds expectations from market data. It proposed pulling the December-2027 CBOT fed funds futures contract (`ZQZ27.CBT`) and converting price to implied rate via `100 − price`, then comparing against `DFEDTARU`/`DFEDTARL` from FRED. We adopted that suggestion.

## Q2 — Cutting-cycle analysis
We initially used a purely algorithmic mask (6-month change in fed funds ≤ −50 bp) to flag "cutting cycle" months. The AI flagged that this produced redundant cycle-start dates (e.g., flagging six consecutive months of a single cycle as "starts"). We took its suggestion to hand-pick the consensus cycle-start dates (1990-07, 1995-07, 1998-09, 2001-01, 2007-09, 2019-08, 2024-09) and report 12-month forward returns from each.

## Q4–6 — Regime construction
We chose the two macro variables (CPI YoY and INDPRO YoY) ourselves; the AI helped with the regime-classification logic, the spell-detection for continuous regimes, and the tabular formatting of the per-regime asset performance summaries.

## Q8 — Weekly bond returns
We re-used the duration-and-carry yield-to-return formula from HW1 and asked the AI to adapt it to weekly frequency (52-period denominator instead of 12). It also pointed out the `both.rolling(52).corr().unstack()` pattern we initially used was returning trivial 1.0 values; the fix was to use `both['Equity'].rolling(52).corr(both['Bond'])`. We adopted that.

## Q9–10 — Risk-parity backtest
We specified the strategy (no leverage, equalize w·σ ignoring covariance, lag weights by one period) and the AI scaffolded the vectorised pandas implementation, the risk-attribution series, and the per-year return summary table. We checked the numbers manually for 2022 against published risk-parity benchmark performance (HFR Risk Parity Vol 10) and the magnitudes line up.
