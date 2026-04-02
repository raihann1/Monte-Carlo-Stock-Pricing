# CSc217 Final Project: Monte Carlo Stock Predictor

This repository contains the final project for CSc217: a Monte Carlo-based stock price forecasting model. The project leverages historical market data to simulate potential future price paths for various equities and ETFs, providing a probabilistic analysis of near-term market behavior.

## Overview
The goal of this project is to model the uncertainty of stock prices using a **Discrete Coin-Flip Monte Carlo Simulation** heavily inspired by Geometric Brownian Motion (GBM). By analyzing historical log returns, the notebook extracts the drift (mean) and volatility (standard deviation) of a stock, and then runs 10,000 simulated trading paths over a specific forward-looking window (e.g., ~64 trading days). 

The project is split into two main phases:
1. **Backtesting (Validation):** Training the model on data from 2014 to early 2024, predicting prices for late 2025, and comparing the simulated distributions against the *actual* historical closing prices to evaluate model efficacy.
2. **Future Prediction:** Training the model on data up to December 2025 to predict potential price ranges and confidence intervals through March 2026.

## Technologies Used
* **Python 3.x**
* **Jupyter Notebook** (`.ipynb`)
* **NumPy:** For vectorized mathematical operations and generating random distributions (coin flips).
* **Pandas:** For time-series data manipulation and rolling window calculations.
* **yfinance:** For pulling historical market data directly via the Yahoo Finance API.
* **Matplotlib:** For visualizing the simulated stock paths alongside expected and actual prices.

## Methodology: The Discrete Coin-Flip Approach
Instead of a continuous-time stochastic differential equation, this project utilizes a simplified discrete-time approach. 

1. Calculate the daily log returns from the training window.
2. Derive $\mu$ (mean of log returns) and $\sigma$ (standard deviation of log returns).
3. For each trading day in the simulation, a "coin flip" (random choice of $+1$ or $-1$) determines the direction of the volatility.
4. The price for the next day is calculated using the formula:
   $X_{t+1} = X_t (1 + \mu \pm \sigma)$
5. This process is repeated across 10,000 independent simulations to build a distribution of final prices.

## Evaluated Assets
The model evaluates a mix of individual tech/retail stocks and broad market indices:
* **$NVDA** (NVIDIA Corporation)
* **$COST** (Costco Wholesale)
* **$DIA** (SPDR Dow Jones Industrial Average ETF)
* **$SPY** (SPDR S&P 500 ETF Trust)
* **$RBLX** (Roblox Corporation)

## Project Output & Statistics
For each ticker, the notebook outputs a statistical summary of the 10,000 simulations and generates a line chart visualizing a subset of the simulated paths.

**Sample Output Metrics:**
* **Simulated Mean Price:** The expected average price at the end of the simulation.
* **Simulated Median Price:** The middle value of all simulated final prices.
* **95% Confidence Interval:** The range in which 95% of the simulated final prices fall (between the 2.5th and 97.5th percentiles).
* **Actual Price (Backtest only):** The real-world recorded price on the end date, used to gauge model accuracy.

## How to Run
1. Open your Jupyter environment (e.g., JupyterLab, Anaconda Navigator, or Google Colab).
2. Open the project `.ipynb` file.
3. Ensure you have the required libraries installed. You can do this by running the following command in a notebook cell:
   `!pip install numpy pandas yfinance matplotlib`
4. Run the cells sequentially from top to bottom to fetch the data, execute the simulations, and generate the plots.
