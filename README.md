**Pfoject Discription & Motivation:**

The Black-Scholes-Merton formula gives a closed-form solution for the price of a European option:

$$C = S \cdot N(d_1) - K e^{-rT} N(d_2),$$

where

$$d_1 = \frac{\ln(S/K) + (r + \frac{\sigma^2}{2})T}{\sigma\sqrt{T}}, \quad d_2 = d_1 - \sigma\sqrt{T}$$

The parameter $\sigma$ stands for the implied volatility (IV).  
It is obtained by numerically inverting BS for each market quote. This inversion is computationally expensive and time-consuming when done for millions of options in real time.

This project aims to build a direct **ML surrogate** that maps observable market features (moneyness, time-to-maturity, bid-ask spread, put-call parity gap, and others) to the implied volatility, effectively replacing Black-Scholes inversion with direct prediction.
The resulting model is also taught to capture the empirically-evidenced volatility smile structure.

The following ML models are considered and estimated: OLS, Ridge with polynomial expansion, Random Forest, and LightGBM. The final model was tuned with Optuna (TPE sampler). 

Results were validated with time-aware GroupKFold CV, bootstrap confidence intervals, and year-by-year stability analysis. The performance result achieved $R_2$ > 0.97 on a chronological test set.

**Dataset:**

*SPY (S&P 500 ETF) daily EOD options, 2010–2023*.  

About 9.5M observations. 10 raw columns; more features (e.g. Greeks) will be computed below.  
*Source: https://www.kaggle.com/datasets/dudesurfin/spy-options-eod-volatility-surface-2010-2023*

**Google Colab**: 
*https://colab.research.google.com/github/stassisss/Finance-projects/blob/main/ML_implied_volatility_predict.ipynb*
