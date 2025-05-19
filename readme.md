# Technical Trading Strategy System

A Python-based trading strategy backtesting system that combines technical indicators (EMA crossovers, ADX, and RSI) to generate buy/sell signals and evaluate strategy performance.

## Overview

This project implements a comprehensive trading strategy system that:
- Fetches historical stock data using Yahoo Finance
- Calculates key technical indicators
- Generates trading signals based on multiple indicator conditions
- Backtests the strategy against historical data
- Provides performance metrics and visualizations

## Features

- **Data Retrieval**: Fetches stock data using yfinance API
- **Technical Indicators**:
  - Exponential Moving Averages (EMA)
  - Average Directional Index (ADX)
  - Relative Strength Index (RSI)
- **Signal Generation**: Combines EMA crossovers, ADX strength, and RSI overbought/oversold conditions
- **Backtesting**: Simulates trades and calculates performance metrics
- **Visualization**: Creates detailed charts for price action, indicators, and performance
- **Performance Analysis**: Calculates key metrics including:
  - Total return
  - Annual return
  - Sharpe ratio
  - Maximum drawdown
  - Number of trades

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/trading-strategy.git
cd trading-strategy

# Install required packages
pip install -r requirements.txt
```

## Requirements

```
pandas
numpy
matplotlib
yfinance
seaborn
```

## Usage

### Basic Example

```python
from trading_strategy import TradingStrategy

# Create strategy instance
strategy = TradingStrategy(ticker="AAPL", period="1y", interval="1d")

# Fetch data and calculate indicators
strategy.fetch_data()
strategy.calculate_indicators()

# Generate signals and backtest
strategy.generate_signals()
strategy.backtest_strategy(initial_capital=10000)

# Display results
strategy.summary()
strategy.plot_results()
plt.show()
```

### Customizing Parameters

```python
# Create strategy with custom parameters
strategy = TradingStrategy(ticker="MSFT", period="2y", interval="1d")

# Calculate custom indicators
strategy.calculate_indicators(
    fast_ema=8,       # Fast EMA period
    slow_ema=21,      # Slow EMA period
    adx_period=14,    # ADX period
    rsi_period=14     # RSI period
)

# Generate signals with custom thresholds
strategy.generate_signals(
    adx_threshold=20,  # Minimum ADX value for trend strength
    rsi_buy=35,        # RSI threshold for buy signals
    rsi_sell=65        # RSI threshold for sell signals
)

# Backtest with custom capital
strategy.backtest_strategy(initial_capital=50000)
```

## Strategy Logic

The trading strategy uses the following logic:

1. **Buy Signal** is generated when:
   - Fast EMA crosses above the Slow EMA
   - ADX is above the threshold (default: 25), indicating a strong trend
   - RSI is below the oversold threshold (default: 30)

2. **Sell Signal** is generated when:
   - Fast EMA crosses below the Slow EMA
   - ADX is above the threshold, indicating a strong trend
   - RSI is above the overbought threshold (default: 70)

## Performance Metrics

The backtest calculates the following performance metrics:

- **Total Return**: Overall percentage gain/loss
- **Market Return**: Buy-and-hold return for comparison
- **Annual Return**: Annualized return percentage
- **Sharpe Ratio**: Risk-adjusted return measure (assuming zero risk-free rate)
- **Max Drawdown**: Maximum percentage decline from peak to trough
- **Number of Trades**: Total buy/sell signals generated

## Visualization

The `plot_results()` method creates three main charts:
1. Price chart with EMA lines and buy/sell signals
2. Technical indicators (ADX and RSI) with threshold lines
3. Cumulative returns comparing strategy performance to buy-and-hold

## Limitations

- The strategy assumes transactions occur at the close price
- No transaction costs or slippage are considered
- No position sizing or risk management beyond basic entry/exit
- Limited to single-instrument trading

## Future Improvements

- Add support for transaction costs and slippage
- Implement position sizing and risk management
- Add parameter optimization functionality
- Support for multi-asset portfolio strategies
- Include additional technical indicators and signal types

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
