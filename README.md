# Miner v1.4 (Commission-Aware)  

**Author:** Arjun1337  
**Version:** 1.4  
**Platform:** MetaTrader 5 (MT5)  
**Type:** Expert Advisor (EA)  

---

## Overview

Miner v1.4 is a commission-aware Forex Expert Advisor designed for systematic trading with hedging capabilities. It uses a dual EMA strategy to identify trends and manages risk through layered hedging and dynamic profit allocation. The EA also features a real-time dashboard displaying trading metrics.

Key features:  
- Trend detection using fast and slow EMAs.  
- Commission-aware profit calculation.  
- Automatic hedge placement with FIFO resolution.  
- Layer-based trade management (BASE & HEDGE trades).  
- Breakeven stop-loss adjustments for risk management.  
- Configurable profit target and maximum hedge count.  
- Real-time on-chart dashboard displaying account and trading metrics.  

---

## Inputs

| Parameter | Description | Default |
|-----------|-------------|---------|
| `IN_EMA_FAST` | Fast EMA period | 5 |
| `IN_EMA_SLOW` | Slow EMA period | 9 |
| `IN_TP_POINTS` | Take Profit distance in points | 30 |
| `IN_HEDGE_DISTANCE_PTS` | Adverse movement distance to trigger hedge | 100 |
| `IN_LOT` | Base trade lot size | 0.01 |
| `IN_PROFIT_TARGET` | Profit target in account currency | 100.0 |
| `IN_MAX_HEDGES` | Maximum simultaneous hedge trades | 3 |
| `IN_MAGIC_BASE` | Magic number for base trades | 123456 |
| `IN_MAGIC_HEDGE` | Magic number for hedge trades | 654321 |
| `IN_TF` | Timeframe for EMA calculation | PERIOD_CURRENT |
| `BE_Target1` | % of TP distance to trigger 1st breakeven | 0.60 |
| `BE_Level1` | % of TP distance for SL at 1st breakeven | 0.40 |
| `BE_Target2` | % of TP distance to trigger 2nd breakeven | 0.80 |
| `BE_Level2` | % of TP distance for SL at 2nd breakeven | 0.60 |

---

## Trading Logic

1. **Trend Detection**:  
   - Compares fast and slow EMA values on closed candles.  
   - `CurrentTrend = 1` → bullish, `-1` → bearish, `0` → flat.

2. **Base Trade Management**:  
   - Opens market orders in the direction of the trend.  
   - Each base trade is layered (`BASE_L<id>`) for tracking.

3. **Hedging**:  
   - Hedge trades (`HEDGE_L<id>_for_<ticket>`) are placed when adverse price movement exceeds `IN_HEDGE_DISTANCE_PTS`.  
   - Maximum hedge trades enforced (`IN_MAX_HEDGES`).  
   - Hedged positions are resolved FIFO with HedgeBuffer allocation.

4. **Profit Allocation**:  
   - Realized profits are split into `ProfitPool` and `HedgeBuffer`.  
   - Losses reduce buffers before affecting account balance.

5. **Breakeven Logic**:  
   - Automatically adjusts stop-loss based on profit percentage thresholds (`BE_Target1/2`).  

6. **Dashboard**:  
   - Displays metrics like Benchmark, ProfitTarget, Base/Hedge trades, HedgeBuffer, ProfitPool, Net Profit, Next Layer ID, and Trading Status.  

---

## Installation

1. Copy the `Miner_v1.4.mq5` file into the `Experts` folder of your MetaTrader 5 installation:  <MT5 Folder>\MQL5\Experts\
2. Compile the EA in the MetaEditor.  
3. Attach it to a chart of your preferred symbol and timeframe.  
4. Configure input parameters as desired.  

---

## Usage Notes

- Ensure your account supports hedging.  
- Always backtest the EA on a demo account before live deployment.  
- Recommended to use a timeframe matching your trading style.  
- Monitor the dashboard for active layers and hedges.  

---

## License

MIT License – free to use, modify, and distribute.  

---

## Disclaimer

Trading Forex carries a high level of risk. Past performance is not indicative of future results. Use this EA at your own risk. Always test on demo accounts before going live.

