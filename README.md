# Stock Backtesting Engine

A professional Python backtesting framework for evaluating moving average crossover strategies on real market data. Built with object-oriented design, this system computes institutional-grade performance metrics including Sharpe Ratio, CAGR, and Maximum Drawdown.

---

## What It Does

This engine downloads real historical stock data, generates systematic buy/sell signals using moving average crossovers, simulates trading performance, and produces a full performance report with visualizations — all in a single function call.

```python
bt = Backtest("AAPL", "2020-01-01", "2024-01-01", short=20, long=50)
bt.run()
```

---

## Performance Metrics

| Metric | Description |
|--------|-------------|
| **Sharpe Ratio** | Risk-adjusted return (annualized) |
| **CAGR** | Compound Annual Growth Rate |
| **Max Drawdown** | Worst peak-to-trough loss |
| **Strategy vs Benchmark** | Performance vs buy-and-hold |

---

## Charts Generated

- **Price + Moving Averages** — visualizes SMA crossover signals
- **Strategy vs Market** — equity curve comparison starting from $100
- **Drawdown Chart** — shows worst losing periods over time

---

## How It Works

```
Real Stock Data (yfinance)
        ↓
Calculate SMA20 + SMA50
        ↓
Generate Buy/Sell Signals (crossover)
        ↓
Apply shift(1) — eliminates look-ahead bias
        ↓
Calculate daily strategy returns
        ↓
Compute Sharpe Ratio, CAGR, Max Drawdown
        ↓
Plot equity curve, drawdown, moving averages
```

---

## Key Engineering Decisions

**Look-ahead bias prevention** — signals are shifted forward by one day using `shift(1)`, ensuring the strategy only acts on information available at the time of trading. This is a common mistake in backtesting that inflates results.

**Vectorized operations** — all calculations use NumPy and Pandas vectorization instead of loops, making the engine fast and scalable to any time period or dataset.

**OOP architecture** — the system is built as a clean class with separate methods for data fetching, signal generation, performance calculation, and visualization. Each method builds on the previous, making the code modular and extensible.

---

## Installation

```bash
pip install numpy pandas matplotlib yfinance
```

---

## Usage

```python
from backtest import Backtest

# Run backtest on any stock
bt = Backtest(
    ticker="AAPL",
    start="2020-01-01",
    end="2024-01-01",
    short=20,   # fast moving average window
    long=50     # slow moving average window
)

bt.run()
```

**Try different stocks and parameters:**

```python
# Test on different tickers
Backtest("GOOG", "2020-01-01", "2024-01-01").run()
Backtest("MSFT", "2020-01-01", "2024-01-01").run()

# Test different MA windows
Backtest("AAPL", "2020-01-01", "2024-01-01", short=10, long=30).run()
Backtest("AAPL", "2020-01-01", "2024-01-01", short=50, long=200).run()
```

---

## Tech Stack

- **Python 3.x**
- **NumPy** — vectorized mathematical operations
- **Pandas** — time-series data manipulation
- **Matplotlib** — performance visualization
- **yfinance** — real market data

---

## Project Structure

```
stock-backtesting-engine/
│
├── BACKTEST.ipynb     # Full implementation + analysis
├── backtest_results.png   # Generated performance chart
└── README.md
```

---

## Author

**Abhishek Paul** — CS Student at CUNY Queens College  
GitHub: [Abhi9267](https://github.com/Abhi9267)  
LinkedIn: [abhipaul768](https://linkedin.com/in/abhipaul768)
