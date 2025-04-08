# Algorithmic-Trading-Bot

Algorithmic trading employs automated strategies that execute trades based on predefined mathematical rules and models. These computer-driven approaches enable transactions at unprecedented speed and frequency, surpassing human capabilities. By systematically following precise guidelines around timing, price, and volume, algo-trading not only creates potential profit opportunities but also enhances market liquidity and reduces emotional decision-making in trading.

## Methodology and Research Design

The project aims to evaluate the predictive performance of different machine learning (ML) algorithms for Bitcoin trading.

The proposed trading strategy integrates key technical indicators, including the **Relative Strength Index (RSI)**, **Simple and Exponential Moving Averages**, and the **Moving Average Convergence Divergence (MACD)**. 

Additionally, the analysis will account for market **seasonality** and underlying **trend patterns**.

We will train **XGBoost**, **Random Forest**, and **LightGBM** models using historical Bitcoin price data, and then conduct a thorough evaluation of their predictive performance.

## Data Acquisition

The historical Bitcoin price data were collected from the **Coinbase API** (**[bitcoin data download](Notebook/03.Download-Bitcoin-Data.ipynb)**). 

The data contains the **hourly** values for the **opening**, **closing**, **high**, **low** price of Bitcoin as well as the **traiding volume**.

The data period spans **1 year**, from **November 2023** to **October 2024**.

## Feature Engineering

### 1. Seasonality and Trends 

- We extract various components of the datetime, such as the month, day, hour, and day of the week. This can help the model capture seasonality and trends.

### 2. STL (Seasonal-Trend decomposition using LOESS)

- **STL** stands for **Seasonal-Trend decomposition using LOESS**. It's a robust statistical method used to decompose a time series into three components:

    1. **Seasonal Component**: Represents the repeating pattern in the data over a fixed period (e.g., daily, weekly, monthly).
    2. **Trend Component**: Captures the long-term progression in the data, showing an overall increase, decrease, or stability over time.
    3. **Remainder/Residual Component**: Represents the part of the data that cannot be attributed to either seasonality or trend, often considered as noise.

### 3. Autocorrelation

- Autocorrelation in time series refers to the correlation of a time series with a lagged version of itself. It measures how past values of the series influence current values. Understanding autocorrelation can help identify patterns, trends, and periodicity in time-series data

### 4. Technical Indicators

- Calculate the values and add new columns with calculated values for **RSI**, **MACD**, **Moving Averages**.

## Model Selection

For our imbalanced dataset, an appropriate model needs to either inherently handle class imbalance or be complemented by techniques to mitigate the issue. We will focus on three models:  **Random Forest**, **XGBoost** and **LightGBM**.

## Conclusion

In this project we tried to find a suitable ML model that could predict the Bitcoin market movements.

A trading strategy was implemented that generates buy/sell signals with the help of some technical indicators.

In a further step, 3 ML models (Random Forest, XGBoost and LightGBM) were examined to see if they could predict the results of this strategy.
Because the target variable is very unbalanced (1 class has over 95% of the values), the three models could not perform very well.

To improve the results, two oversampling methods (SMOTE and ADASYN) were used. In addition, the weight of the individual classes was changed during hyper-parameter tuning with Optuna in order to improve the ratio of the classes. These measures have improved the F1-Score (Macro), but the values have remained quite low.

**LightGBM** performed best with **SMOTE** oversampling.