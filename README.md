# HVAC Power Usage Time Series Analysis

## Problem Statement

This project focuses on analyzing synthetic HVAC power usage data to uncover patterns, detect seasonality, assess autocorrelation, and develop predictive models. The ultimate goal is to understand the structure and behavior of energy usage over time to aid in forecasting and optimization efforts.

---

## Dataset Summary

- **Size:** 408,000 data points
- **Features:** 45 variables
- **Sampling Frequency:** 15-minute intervals
- **Time Range:** From `2020-01-01 00:00:00` to `2031-08-20 23:45:00`

### Key Preprocessing Steps

- **Zero-Variance Features Removed:**
  - `hvac_control`, `cooling_demand`, `hvac_control_sma`, `cooling_demand_sma`,  
    `hvac_control_ema`, `cooling_demand_ema`, `hvac_control_minmax`, `cooling_demand_minmax`
  
- **Perfectly Correlated Features Identified and Removed:**  
  Features with perfect positive or negative correlation were dropped to avoid multicollinearity and redundancy.

- **Feature Engineering and Reduction:**
  - Removed duplicated transformed variables including SMA, EMA, Min-Max, Savitzky-Golay, and Robust filters when redundant.
  - Focused on selecting features based on their relevance and independence.

---

## Tools and Technologies Used

- **Languages & Libraries:**
  - Python
  - pandas, numpy – for data manipulation
  - matplotlib, seaborn – for data visualization
  - statsmodels – for time series decomposition, ADF test, and autocorrelation analysis
  - scikit-learn – for regression modeling and evaluation
  - pmdarima – for automated ARIMA modeling

- **Statistical Tests & Modeling:**
  - Seasonal Decomposition (`seasonal_decompose`)
  - Augmented Dickey-Fuller Test (`adfuller`)
  - Autocorrelation and Partial Autocorrelation (ACF, PACF)
  - Ljung-Box Test (`acorr_ljungbox`)
  - Regressors: `LinearRegression`, `RandomForestRegressor`, `GradientBoostingRegressor`

---

## Challenges

- **High Dimensionality:**  
  Managing 45 features, many of which were transformations of the same base variables, required thoughtful feature selection and dimensionality reduction.

- **Redundant Data:**  
  Several features were either constant or perfectly correlated, necessitating a rigorous correlation analysis and cleaning process.

- **Stationarity Assumption for Time Series Models:**  
  Although the ADF test confirmed stationarity of power usage, lack of autocorrelation (confirmed via ACF, PACF, and Ljung-Box test) limited the usefulness of some traditional time series models like ARIMA.

- **Seasonality Considerations:**  
  Strong yearly seasonality in outdoor temperature prompted further investigation into similar patterns in power usage. However, the usage data lacked significant autocorrelation, complicating seasonal modeling.

---

## Summary of Findings

- Power usage is stationary (ADF test p-value = 0.0).
- No significant autocorrelation was found (Ljung-Box p-value = 0.70).
- Feature selection and transformation significantly improved data quality for modeling.
- Dataset contains high-frequency data with clear seasonal trends in temperature but not in power usage.

---

*This analysis lays the groundwork for future modeling steps focused on feature-specific predictions and deeper causal inference.*
