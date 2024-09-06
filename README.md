# ECON 409 Project: Two Approaches to Forecasting GBP/USD: Molodtsova-Papell and Kalman Filters

## Overview

In this project, we develop two strategies to forecast the GBP/USD exchange rate: one using a modified Fisher Equation proposed by Molodtsova-Papell (2012) to explore relationships between exchange rates, inflation, and industrial production, and the other employing a Kalman filter to estimate interest rate differentials between the U.S. and U.K. We segment the data into training and deployment sets to simulate real-world conditions, aiming to evaluate the real-time efficiency of our models. 

## First Approach - Molodtsova-Papell
In our first approach, we modify the Molodtsova & Papell (2012) model, utilizing the Taylor-rule fundamentals to forecast the GBP/USD exchange rate. We make two key changes: substituting the Consumer Price Index (CPI) with the Personal Consumption Expenditures (PCE) price index and replacing GDP with the Industrial Production Index (IPI) due to the quarterly frequency of GDP data. We calibrate our model with these variables and use OLS to estimate exchange rate changes, leading to a final trading strategy. Although the model yields a 5% profit, statistical tests (Diebold-Mariano and Clark-West) indicate that it does not outperform the random walk.

### Variables Used:
1. **GBP/USD Exchange Rate** - The target variable for forecasting.
2. **PCE Price Index** - Used as a measure of inflation, replacing CPI.
3. **Industrial Production Index (IPI)** - Used as a proxy for GDP.
4. **Hyperparameters (hus and huk)** - Window sizes for calculating the output gap for industrial production in the UK and the US.
5. **∆sˆt+1** - Estimated log change in the GBP/USD exchange rate for time t + 1.
6. **Mean Squared Error (MSE)** - Used for tuning hyperparameters.
7. **Diebold-Mariano (DM) Test Statistic** - Used to compare model performance against a random walk.
8. **Clark-West (CW) Test Statistic** - Also used to compare model performance against a random walk.

## Second Approach -  Kalman Filters
In our second approach, we implement a "manual" Kalman filter to estimate the interest rate differential (IRD) between the U.S. and U.K. and use the Econ 409 Strategy to forecast directional movements in the GBP/USD exchange rate. We manually build the Kalman filter, tuning the Process Noise (Q), Measurement Noise (R), and the rolling window size (T) to optimize our trading strategy based on the Sharpe Ratio. The optimal parameters were applied to testing data, resulting in an 11.3% profit. While the Binomial test suggests that our strategy captures directional changes in the exchange rate, the Weighted Binomial test indicates it may not effectively capture large movements.

### Variables Used:
1. **Interest Rate Differential (IRD)** - The primary variable estimated using the Kalman filter.
2. **Kalman Filter Parameters:**
   - **Process Noise (Q)** - A tuned hyperparameter essential for the Kalman gain calculation.
   - **Measurement Noise (R)** - Another tuned hyperparameter essential for the Kalman gain calculation.
   - **Kalman Gain (Kt)** - Determined by the process and measurement noise at any given time.
3. **Rolling Window Size (T)** - Used for calculating the rolling mean and standard deviation in the trading strategy.
4. **Surprise (ε̄t)** - The difference between the observed data and the Kalman filter's prediction.
5. **Sample Mean (μˆt)** - The mean of surprises on a rolling window of size T.
6. **Sharpe Ratio** - Used as the performance metric for tuning the Kalman filter parameters.
7. **Equity Curve** - The cumulative profit/loss from applying the strategy.
8. **Binomial Test Statistic (TB)** - Used to test the effectiveness of the directional forecasts.
9. **Weighted Binomial Test Statistic (TWB)** - Used to test the effectiveness of the strategy in capturing large directional movements in the exchange rate.

## Findings

Both of our strategies failed to outperform the Hedge Fund Research Index (HFRI) in key metrics such as geometric average monthly returns, annualized returns, Sharpe ratios, and the percentage of winning months. Our strategies exhibited higher risk, with larger standard deviations, annualized standard deviations, and significant maximum drawdowns, especially for the Kalman filter. Despite being less correlated with the S&P 500, our strategies' poor performance indicates that adjustments are necessary. Future improvements could include optimizing the training data length, tuning hyperparameters using alternative metrics like the Sharpe ratio, or adopting real-time data responses and multivariate approaches to improve robustness

## References

- Tanya Molodtsova and David H. Papell. Taylor rule exchange rate forecasting duringthe financial crisis. NBER International Seminar on Macroeconomics, 9(1), 2012. [Link to paper](https://www.nber.org/papers/w18330).

5. Run the analysis scripts:
    ```bash
    python merged.ipynb
    ```
