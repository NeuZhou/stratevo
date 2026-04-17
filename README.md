<div align="center">
<br>

# 🦀 StratEvo

**Stop writing trading strategies. Evolve them.**

A genetic algorithm engine that breeds and walk-forward validates trading strategies across 484+ market factors.

<p align="center">
  <img src="https://img.shields.io/badge/evolvable_factors-484+-orange" alt="484+ Evolvable Factors">
  <img src="https://img.shields.io/badge/markets-US_Stocks_%7C_Crypto-blue" alt="Markets">
  <img src="https://img.shields.io/badge/validation-Walk--Forward_%7C_Monte_Carlo-green" alt="Validation">
  <a href="https://discord.gg/kAQD7Cj8"><img src="https://img.shields.io/discord/1488800950696284272?color=7289da&label=Discord&logo=discord&logoColor=white" alt="Discord"></a>
</p>

<p>
  <a href="#-live-signals">Live Signals</a> ·
  <a href="#-paper-trading-performance">Paper Trading</a> ·
  <a href="#how-it-works">How It Works</a> ·
  <a href="#evolution-results">Results</a> ·
  <a href="#anti-overfitting">Robustness</a> ·
  <a href="#get-access">Get Access</a>
</p>

</div>

---

## 📡 Live Signals

> Real-time buy/sell signals from our evolved strategies. Updated daily. All signals are recorded in git history — **immutable and verifiable**.

### Latest Signals

<!-- SIGNALS_START -->
| Date | Market | Action | Asset | Entry Price | DNA | Status |
|------|--------|--------|-------|-------------|-----|--------|
| *Signals will be posted here as Paper Trading goes live* | | | | | | |
<!-- SIGNALS_END -->

📁 **Full signal history:** [`signals/`](signals/)

---

## 📊 Paper Trading Performance

> Forward-testing evolved strategies with real market data, simulated execution. No hindsight, no cherry-picking.

### Current Paper Portfolio

<!-- PAPER_START -->
| Strategy | Market | Start Date | Days | Return | Sharpe | MaxDD | Trades | Status |
|----------|--------|------------|------|--------|--------|-------|--------|--------|
| *Paper Trading launching soon — engines currently evolving* | | | | | | | | |
<!-- PAPER_END -->

📁 **Daily P&L reports:** [`paper-trading/`](paper-trading/)  
📈 **Equity curves:** [`paper-trading/charts/`](paper-trading/charts/)

---

## How It Works

Most quant tools make you **write** the strategy. StratEvo **evolves** them.

```
You write the rules        →  StratEvo discovers the rules
You tune parameters        →  GA tunes parameters  
You test on one period     →  Walk-forward tests on multiple windows
You hope it generalizes    →  Monte Carlo measures if it does
```

```
  Random DNA population (484 factor weights + risk parameters)
       │
       ▼
  ┌──────────────────────┐
  │  Walk-Forward Test   │  Multi-window out-of-sample validation
  │  each DNA candidate  │  Real fees, slippage, position caps
  └──────────┬───────────┘
             │
             ▼
  Keep the survivors (fitness = Sharpe × Return / MaxDD)
             │
             ▼
  Mutate + Crossover → next generation
             │
             ▼
  Repeat for N generations
```

Each DNA is a weight vector across 484+ factors **plus** risk/position parameters — all evolvable:

| Parameter | Range | What it controls |
|-----------|-------|-----------------|
| Factor weights (×484) | 0.0–1.0 | Which factors matter and how much |
| `hold_days` | 2–60 | Day trades through swing trades |
| `trailing_stop` | % | Lock in profits, trail below peak |
| `market_regime` | sensitivity | Auto-reduce exposure in bear markets |
| `kelly_fraction` | 0–1 | Position sizing based on recent win rate |

---

## Evolution Results

> Numbers from our running evolution engines. Updated regularly.

### 🇺🇸 US Stocks (100 S&P 500 stocks — Gen 94)

| Metric | Best DNA |
|:------:|:--------:|
| Annual Return | **33.5%** |
| Sharpe Ratio | **1.47** |
| Max Drawdown | 17.0% |
| Win Rate | 55.5% |
| Profit Factor | 1.75 |
| Total Trades | 179 |

### ₿ Crypto (17 assets — Gen 44)

| Metric | Best DNA |
|:------:|:--------:|
| Annual Return | **77.2%** |
| Sharpe Ratio | **3.25** |
| Max Drawdown | 15.7% |
| Win Rate | 52.3% |
| Profit Factor | 1.73 |
| Total Trades | 194 |

**Caveats:** These are backtests with walk-forward validation, not live trades. That's why we're running Paper Trading — to prove it works forward, not just backward.

---

## Anti-Overfitting

We learned the hard way. An early version showed 25,000% returns — it was a bug (look-ahead bias).

| Defense | What it does |
|---------|-------------|
| **Walk-Forward** | Multi-window OOS validation. Must profit on data it never trained on. |
| **Monte Carlo** | 1,000 shuffled iterations. p-value < 0.05 or it's luck. |
| **CPCV** | Combinatorial Purged Cross-Validation — industry standard. |
| **Arena Mode** | Multiple strategies compete. Crowded signals get penalized. |
| **Bias Detection** | Look-ahead, snooping, survivorship — flagged automatically. |
| **Turnover Penalty** | Excessive trading punished. Real transaction costs modeled. |

Honest 33% > fake 25,000%.

---

## 484+ Factors

| Category | Count | Examples |
|----------|------:|---------|
| Crypto-Native | 200 | Funding rate, whale detection, liquidation cascade |
| Momentum | 14 | ROC, acceleration, trend strength |
| Volume & Flow | 13 | OBV, smart money, Wyckoff VSA |
| Volatility | 13 | ATR, Bollinger squeeze, vol-of-vol |
| Mean Reversion | 12 | Z-score, Keltner channel position |
| Trend Following | 14 | ADX, EMA golden cross, MA fan |
| Qlib Alpha158 | 11 | Microsoft Qlib compatible factors |
| + 5 more categories | 37 | Risk, quality, price structure, sentiment, DRL |

All factor weights discovered by evolution — zero manual tuning.

---

## Strategy Styles

The algorithm converges on recognizable trading styles:

| Style | What the DNA Learned |
|-------|---------------------|
| **Value Seeker** | Buys cheap, holds patient |
| **Momentum Rider** | Chases what's moving, cuts what isn't |
| **Mean Reverter** | Bets on bounce-backs |
| **Flow Reader** | Follows the money — volume precedes price |
| **Volatility Hunter** | Profits from vol expansion |
| **Crypto Native** | 200 factors for 24/7 markets |

---

## Get Access

StratEvo Pro includes the full evolution engine, paper trading, signal generation, and live exchange connectors.

📧 **Contact:** [neuzhou@outlook.com](mailto:neuzhou@outlook.com)  
💬 **Discord:** [discord.gg/kAQD7Cj8](https://discord.gg/kAQD7Cj8)

---

## Technical Papers

- [GT-Score: A Generalizable Fitness Function for Walk-Forward Strategy Evolution](https://arxiv.org/abs/2602.00080)

---

<div align="center">

**The strategies evolve. The signals speak for themselves.**

*Check back daily for updated signals and paper trading results.*

</div>
