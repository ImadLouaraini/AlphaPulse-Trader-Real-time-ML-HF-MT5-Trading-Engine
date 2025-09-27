# AlphaPulse-Trader-Real-time-ML-HF-MT5-Trading-Engine
AlphaPulse Trader is a high-frequency, machine-learning-driven trading system for MetaTrader5 (MT5) that leverages real-time price data, predictive ML models, and advanced money management to execute optimized trades.

Key Features

High-Frequency Trading (HF):
Real-time tick streaming (~20 updates/sec) for fast trade execution.

Machine Learning with Optuna:
LightGBM model optimized with Optuna for accurate predictive signals.
Background retraining ensures the model adapts to new market conditions.

Vectorized Feature Computation:
Efficient computation for multiple tickers simultaneously to minimize latency.

Barrier & Correlation Signals:
Combines barrier-based trading signals with correlation filtering to reduce risk.

Advanced Money Management:
Dynamic lot sizing, stop-loss, and take-profit management based on account risk.

Modular Architecture:
Clean separation of ML, signals, and execution logic for easy maintenance and extensibility.

# Project Structure

               ┌────────────────────────────┐
               │ live_mt5_hf_optimized.py   │
               │----------------------------│
               │ - Main HF trading loop     │
               │ - Async tick listener      │
               │ - Executes trades          │
               │ - Calls background ML      │
               └─────────────┬─────────────┘
                             │
                             ▼
               ┌────────────────────────────┐
               │     ml_live_optuna.py       │
               │----------------------------│
               │ - compute_features          │
               │ - train LightGBM (Optuna)  │
               │ - Background retraining     │
               │ - Model persistence         │
               └─────────────┬─────────────┘
                             │
         ┌───────────────────┴───────────────────┐
         ▼                                       ▼
┌─────────────────────┐                  ┌────────────────────────┐
│     signals.py      │                  │ money_management_mt5.py│
│---------------------│                  │------------------------│
│ - Barrier signals   │                  │ - Lot sizing           │
│ - Correlation filter│<---------------->| - SL/TP computation    │
│ - Trading logic     │                  │ - Risk per trade       │
└─────────────────────┘                  └────────────────────────┘
                             ▲
                             │
                             ▼
                  x ┌───────────────────┐
                   │   DataHandler      │
                   │------------------- │
                   │ - Fetch historical │
                   │   & live data      │
                   │ - Maintain price_df│
                   └───────────────────┘

                   └───────────────────┘



# Usage

1-Install dependencies:

pip install pandas numpy lightgbm MetaTrader5 optuna


2-Configure account & tickers in live_mt5_hf_optimized.py.

3-Run the live trading system:   python live_mt5_hf_optimized.py


4- Monitor the console for signals, executed trades, and live updates.

# Notes

Supports multiple currency pairs with correlation-aware trading.

Designed for educational and research purposes; backtest before live trading.

Modular design allows future extensions for stocks, options, or portfolio-level trading.
