# Trader Behavior vs Market Sentiment Analysis

This project explores the relationship between trader behavior and market sentiment using real trading data and the Fear–Greed Index.  
It reconstructs positions, computes realized PnL, and compares performance across sentiment regimes (Fear, Neutral, Greed).

---

## Objective

Analyze how trader profitability, risk, and activity patterns change with market sentiment.

### Key Questions
- Do traders behave differently during “Fear” vs “Greed”?
- Which regime provides the best execution quality and hit rate?
- How do regime transitions affect trading outcomes?

---

## Data

### Trade Data (`historical_data.csv`)
- **Columns:** `Execution`, `Size Token`, `Size USD`, `Side`, `Timestamp`, `Fee`, `Order ID`, etc.  
- Each row represents one executed trade (fill).

### Sentiment Data (`fear_greed_index.csv`)
- **Columns:** `timestamp`, `value`, `classification`, `date`.  
- Daily sentiment from the crypto Fear–Greed Index.  
- Forward-filled intraday for trade matching.

---

## Methodology

### Data Preparation
- Clean duplicates and drop invalid rows.  
- Unify timestamps to UTC.  
- Use `size_usd` as notional; compute as `qty × price` if missing.

### Inventory and PnL Reconstruction
- Apply average-cost accounting per `account–coin` pair.  
- Compute realized PnL only on closing trades (sells that reduce position).  
- Track realized quantity, realized notional, and fees.

### Sentiment Join
- Forward-fill daily sentiment values to trade timestamps.  
- Identify regime transitions (e.g., Fear → Greed, Greed → Neutral).

### Metrics by Regime
- **Win Rate:** Fraction of closing trades with positive realized PnL.  
- **PnL per Trade:** Mean realized profit or loss per trade.  
- **PnL per Notional:** Return per dollar risked.  
- **Fee % of Notional:** Trading cost.  
- **Trades per Hour:** Behavioral intensity pattern.

### Visualization
- Bar charts for performance metrics.  
- KDE density plots for realized PnL distributions.  
- Time-of-day activity plots.

---

## Key Insights

- **Fear:** High trade volume but lowest profitability. Traders often scale in during volatility spikes.  
- **Greed:** Better relative efficiency; smaller losses per trade and higher win rate.  
- **Neutral:** Low participation and poor results; often an unproductive phase.  
- **After Regime Flips:** Sharp increase in variance; size reductions or cooldown periods are advisable.

---
