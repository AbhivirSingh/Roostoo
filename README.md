# Roostoo-CodeWrappers

This repository contains a sophisticated cryptocurrency trading bot designed to autonomously trade on a mock exchange API provided by Roostoo. The bot implements multiple trading strategies, technical indicators, and risk management techniques to optimize trading performance.

## Features

- **Multi-Strategy Trading**: Supports multiple trading strategies including Mean Reversion, MACD Crossover, RSI, Bollinger Bands, and a Combined Strategy that aggregates signals.
- **Technical Indicators**: Utilizes RSI, MACD, Bollinger Bands, and Stochastic Oscillator for generating trading signals.
- **Coin Selection**: Dynamically selects coins based on historical performance, volatility, and technical signals using data from Yahoo Finance (`yfinance`).
- **Risk Management**: Implements stop-loss, take-profit, and position sizing based on portfolio risk percentage.
- **Mock API Integration**: Interacts with the Roostoo mock API for market data, balance, and order placement.
- **Trade Logging**: Saves detailed trade logs with timestamps, actions, prices, and profit/loss details.
- **Performance Metrics**: Tracks portfolio value, Sharpe ratio, and win rate for performance evaluation.

## Prerequisites

- Python 3.8+
- Required Python packages (install via `pip`):

  ```bash
  pip install requests pandas numpy yfinance talib
  ```

  Note: `talib` requires additional setup depending on your system. Refer to the TA-Lib documentation for installation instructions.
- A stable internet connection for API and historical data retrieval.

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/crypto-trading-bot.git
   cd crypto-trading-bot
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Ensure `TA-Lib` is properly installed:

   - For Windows, download precompiled binaries or build from source.
   - For Linux/macOS, follow the installation guide in the TA-Lib repository.

## Configuration

The bot's configuration is defined in `trading_bot.py`. Key parameters include:

- **API Settings**:
  - `API_BASE_URL`: Mock API endpoint (`https://mock-api.roostoo.com`).
  - `API_KEY` and `SECRET_KEY`: Credentials for API authentication (pre-filled for mock API).
- **Trading Parameters**:
  - `POSITION_SIZE_PCT`: Risk 5% of portfolio per trade.
  - `STOP_LOSS_PCT`: 3% stop loss.
  - `TAKE_PROFIT_PCT`: 6% take profit.
  - `MAX_COINS`: Maximum of 5 coins to trade simultaneously.
  - `FETCH_INTERVAL`: 10 seconds between market data fetches.
  - `TRADING_INTERVAL`: 20 seconds between trading decisions.
- **Technical Indicator Parameters**:
  - Configurable periods for RSI, MACD, Bollinger Bands, and Stochastic Oscillator.

Modify these parameters in `trading_bot.py` to suit your trading preferences.

## Usage

1. Run the bot:

   ```bash
   python trading_bot.py
   ```

2. The bot will:

   - Connect to the Roostoo mock API.
   - Fetch market data and select coins.
   - Execute trades based on the configured strategies.
   - Log trades to a file (`trade_log_YYYYMMDD_HHMMSS.txt`).
   - Continue running until manually stopped (`Ctrl+C`).

3. Upon termination, the bot:

   - Closes all open positions.
   - Saves a final trade log.
   - Outputs performance metrics (final portfolio value, Sharpe ratio, win rate).

## File Structure

- `trading_bot.py`: Main script containing the trading bot logic.
- `trade_log_*.txt`: Generated trade log files with detailed trade information.
- `requirements.txt`: List of Python dependencies.

## Trading Strategies

The bot supports the following strategies, selectable dynamically based on performance:

1. **Mean Reversion**: Buys when price is below the mean, sells when above.
2. **MACD Crossover**: Trades based on MACD line crossing the signal line, with RSI confirmation.
3. **RSI Strategy**: Buys on oversold RSI (&lt;30) and sells on overbought RSI (&gt;70), with Stochastic Oscillator confirmation.
4. **Bollinger Bands**: Buys when price crosses below the lower band, sells above the upper band, with RSI confirmation.
5. **Combined Strategy**: Requires agreement from at least two of MACD, RSI, and Bollinger Bands strategies.

## Risk Management

- **Position Sizing**: Limits trade size to 5% of portfolio, adjusted based on active positions.
- **Stop Loss/Take Profit**: Automatically sets stop-loss (3%) and take-profit (6%) levels for each trade.
- **Sharpe Ratio**: Tracks portfolio performance to evaluate risk-adjusted returns.

## Logging

- Console logs provide real-time updates on coin prices, signals, trades, and portfolio value.
- Trade logs are saved to text files with details on each trade, including:
  - Timestamp, action (BUY/SELL), coin, pair, price, amount.
  - Cash spent/received, commissions, net proceeds, and profit percentage.

## Limitations

- Designed for the Roostoo mock API; real exchange integration requires API modifications.
- Historical data relies on `yfinance`, which may have limitations for certain assets.
- Performance depends on market conditions and parameter tuning.
- No graphical user interface; monitoring is via console and log files.

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/YourFeature`).
3. Commit your changes (`git commit -m "Add YourFeature"`).
4. Push to the branch (`git push origin feature/YourFeature`).
5. Open a pull request.

Please include tests and documentation for new features.

## License

This project is licensed under the MIT License. See the LICENSE file for details.

## Disclaimer

This bot is for educational and simulation purposes only. Trading cryptocurrencies involves significant risk, and this bot is not intended for use with real funds without thorough testing and validation. The author is not responsible for any financial losses incurred.