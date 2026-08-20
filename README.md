# Momentum Martingale Simulator

A Pine Script (v6) indicator for TradingView. This is an **educational/simulation tool** — it is **not a trading strategy meant for actual use**. It shows what would happen if someone played Martingale betting on top of a simple prediction method, using real historical data.

## What it does

### 1. Prediction method (momentum-based)
- Looks at the color of yesterday's candle
- Yesterday green → today's prediction: **BUY**
- Yesterday red → today's prediction: **SELL**
- Assumption: the previous day's direction continues

### 2. Evaluation
- **WIN** if the prediction is confirmed today (e.g. BUY + today's candle is green)
- **LOSS** otherwise

### 3. Martingale betting logic
- Starts with an initial bet (`initialBet`)
- **WIN** → wins the bet, returns to the initial bet amount
- **LOSS** → loses the bet, the next bet is doubled
- If bet > available capital → **BLOWN** (account wipeout, reset to zero)
- If capital ≥ `profitTarget` → **TARGET WIN**

### 4. Yearly reset (optional)
On January 1st, everything restarts from the beginning, and the previous year's result is saved to the history table.

## Inputs

| Parameter | Default | Description |
|---|---|---|
| Initial Capital | $10,000 | Starting point |
| Initial Bet | $100 | Bet size after every WIN, or at the start |
| Profit Target | $15,000 | Above this capital level → "WIN" |
| Reset every January 1st | Yes | Restarts from the beginning every year |
| Show labels | Yes | Labels on candles with WIN/LOSS/BLOWN |
| Labels: last X days | 60 | Limits the labels so the chart doesn't get cluttered |
| Table position/size | — | Purely aesthetic settings |

## What it shows on the chart

- **Capital chart** (bottom panel, `overlay = false`) — the path of the simulated capital, day by day
- **Statistics table** (top right, configurable) — current capital, max bet, current/max losing streak, candle status
- **Yearly history table** (bottom right) — final result for each year (PROFIT / LOSS / WIN / BLOWN)

## The core message

Martingale betting does **not** change the statistical probability of winning — it just increases risk exponentially ($100 → $200 → $400 → $800 → $1,600 …). A sufficiently long losing streak (statistically inevitable over the long run) leads to a total loss of capital, regardless of how "good" the prediction method looks in the short term. This tool exists to show, visually, how quickly that happens, using real data.

## Risk / Disclaimer

This is a simulation using historical data, **not** investment advice or a guarantee of future performance. The prediction method (yesterday's color → tomorrow's direction) has no proven statistical basis (it is not certain that a real momentum edge exists on the daily timeframe), and Martingale staking is one of the most dangerous money management methods that exist. It does not account for slippage, spreads, commissions, or liquidity.

## Installation

1. TradingView → Pine Editor (bottom panel)
2. Paste the code
3. "Save" → "Add to chart"
4. Configure parameters via the gear icon on the indicator
