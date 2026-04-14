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

Results were validated with time-aware GroupKFold CV, bootstrap confidence intervals, and year-by-year stability analysis. The performance result achieved $R_2 > 0.97$ on a chronological test set.

---

**Dataset:**

*SPY (S&P 500 ETF) daily EOD options, 2010–2023*.  

About 9.5M observations. 10 raw columns.  
*Source: https://www.kaggle.com/datasets/dudesurfin/spy-options-eod-volatility-surface-2010-2023*

Implemented in the project via **kagglehub** library:  
path = kagglehub.dataset_download("dudesurfin/spy-options-eod-volatility-surface-2010-2023")

---

**Google Colab**: 
*[https://colab.research.google.com/github/stassisss/Volatility_surface_predict_ML/blob/main/ML_implied_volatility](https://colab.research.google.com/github/stassisss/Volatility_surface_predict_ML/blob/main/ML_implied_volatility)*

-----

**Описание на русском языке:**

Формула Блэка–Шоулза предоставляет аналитическое решение для цены европейского опциона:

$$C = S \cdot N(d_1) - K e^{-rT} N(d_2),$$

где

$$d_1 = \frac{\ln(S/K) + (r + \frac{\sigma^2}{2})T}{\sigma\sqrt{T}}, \quad d_2 = d_1 - \sigma\sqrt{T}$$

Параметр $\sigma$ обозначает подразумеваемую волатильность (IV).
IV вычисляется через обращение формулы BS для каждой рыночной котировки. Однако это обращение является ресурсно затратным и занимает много времени при обработке большого количества даныых (котировок) в реальном времени.

Данный проект нацелен на создании прямого **ML-суррогата**: используя наблюдаемые рыночные характеристики (moneyness, время до экспирации, bid-ask спред, put-call parity и др.), вычисляет подразумеваемую волатильность, фактически заменяя численное обращение формулы Блэка–Шоулза прямым предсказанием.
Полученная модель также обучается улавливать эмпирически наблюдаемую структуру «улыбки волатильности».

В проекте рассматриваются и оцениваются следующие модели машинного обучения: OLS, Ridge с полиномиальным расширением, Random Forest и LightGBM. Финальная модель была настроена с использованием Optuna (TPE).

Результаты были валидированы с помощью кросс-валидации GroupKFold, bootstrap-доверительных интервалов и анализа стабильности по годам. Достигнутый результат качества: $R_2 > 0.97$ на тестовой выборке.

---

**Датасет:**

*SPY (ETF на S&P 500) — ежедневные EOD-данные по опционам, 2010–2023 гг.*

Около 9.5 млн наблюдений. 10 исходных колонок.  
*Источник: [https://www.kaggle.com/datasets/dudesurfin/spy-options-eod-volatility-surface-2010-2023](https://www.kaggle.com/datasets/dudesurfin/spy-options-eod-volatility-surface-2010-2023)*

Датасет скачен через библиотеку **kagglehub**:  
path = kagglehub.dataset_download("dudesurfin/spy-options-eod-volatility-surface-2010-2023")




