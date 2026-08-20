# Momentum Martingale Simulator (Pine Script v6)

A TradingView indicator that simulates a **Martingale** strategy driven by a
simple "momentum" rule: if yesterday's candle was green, it opens a "BUY" for
today; if it was red, it opens a "SELL". Every loss doubles the bet
(martingale), and every win resets the bet back to the initial amount.

⚠️ **This is an educational/simulation tool, not investment advice.**
The Martingale strategy carries a very high risk of a total capital
"blow-up".

## What it does

- Starts with an `Initial Capital` and an `Initial Bet`.
- On each new bar, it compares yesterday's candle color to today's outcome
  and determines a win or a loss.
- On a **win**: capital increases by the current bet, and the bet resets
  back to the initial amount.
- On a **loss**: capital decreases by the current bet, and the next bet
  doubles.
- If the bet would exceed the available capital → "BLOWN UP", capital is
  set to zero and the simulation stops for the current year.
- If capital reaches the `Profit Target` → "TARGET WIN" and the simulation
  stops.
- Optional **reset every January 1st**, with a yearly history table
  (profit/loss/blow-up/target reached for each past year).

## Settings (Inputs)

| Setting | Description |
|---|---|
| Initial Capital ($) | Starting point of the simulated capital |
| Initial Bet ($) | Bet size at the start of each new cycle |
| Profit Target - WIN ($) | Capital level that triggers a "win" |
| Reset every January 1st | Restarts the simulation each new year |
| Show labels on candles | Toggles the on-chart labels |
| Labels: last X days only | Limits how many recent labels are shown (for performance) |
| Table Position | Top Right / Top Left / Top Center |
| Table Text Size | Small / Normal / Large |

## Installing on TradingView

1. Open TradingView → **Pine Editor**.
2. Copy the entire contents of `momentum_martingale_simulator.pine`.
3. Click **Add to Chart**.
4. Adjust the inputs from the indicator's gear icon (⚙️).

## Known limitations

- The "yesterday/today" logic relies on the last two closed candles of
  whatever timeframe you have selected — on intraday timeframes this
  doesn't literally correspond to "days".
- The history table shows up to 25 years.
- Commissions/spread are not accounted for — this is a purely theoretical
  simulation.

## Files

- `momentum_martingale_simulator.pine` — the indicator's source code.
