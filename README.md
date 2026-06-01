# Trader Performance vs Market Sentiment

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Jaswanth-K1210/sentiment-trader-analysis/blob/main/sentiment_trader_analysis.ipynb)

Data science assignment for the Primetrade.ai internship. The goal was to explore how trader performance relates to Bitcoin market sentiment, find patterns that aren't obvious on the surface, and turn them into trading-strategy insights.

## Datasets

- `fear_greed_index.csv` — daily Bitcoin Fear/Greed Index (Extreme Fear, Fear, Neutral, Greed, Extreme Greed)
- `historical_data.csv` — ~211k Hyperliquid trade fills (account, coin, execution price, size, side, direction, closed PnL, fee, timestamp)

## How to run

1. Open the notebook in Google Colab (badge above) or download `sentiment_trader_analysis.ipynb`
2. Run the first cell and upload both CSVs when prompted
3. Run all cells top to bottom

## Approach

Each trade is joined to its day's sentiment on calendar date (100% of trades matched). I then group by sentiment regime and compare performance and behaviour: average and median PnL, win rate, position size, long/short bias, and the correlation between sentiment and daily PnL. The sentiment is analysed both as the full 5-class scale and as a collapsed Fear/Greed view.

## Key findings

1. Profit per trade is highest in **Extreme Greed**, not Fear — best win rate (~46%) but on the smallest average position size.
2. Traders **over-size during Fear**. Fear days have the biggest median positions and the highest total PnL, but that's driven by volume and size, not a per-trade edge — the win rate in Fear is below Extreme Greed.
3. Positioning is **contrarian**: roughly 64–68% of trades are long during Fear versus 42–49% long during Greed. The crowd buys fear and de-risks in greed.
4. Sentiment value is a **weak direct predictor** of daily PnL (correlation near zero). It shapes how people size and position far more than it drives the outcome.
5. **Neutral is the lowest-edge regime.** The signal lives in the extremes, not the middle.

## Strategy takeaways

The notebook ends with a sentiment-to-action table and these rules:
- Cut position size during Fear — traders over-bet there without a matching edge.
- Keep positions small and disciplined in Extreme Greed, where the realised win rate is highest.
- Treat Neutral as a low-edge regime and reduce activity.
- Use sentiment as a sizing and risk governor, not as a standalone directional signal.

## Notes

- The brief mentioned a leverage column; it isn't in this export, so Size USD is used as the risk-appetite proxy.
- Closed PnL of 0 rows are opening fills with no realised PnL yet.
- A natural next step is a multi-factor model combining sentiment with volatility and funding rates.

## Tech

Python, pandas, numpy, matplotlib, seaborn.
