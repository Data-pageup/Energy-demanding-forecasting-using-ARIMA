
# Time Series Analysis and Forecasting with ARIMA

##  Project Overview

This project focuses on forecasting electrical load demand and solar power generation in Italy using ARIMA (AutoRegressive Integrated Moving Average) models. The analysis uses real-world time series data from 2016 to predict future energy patterns, which is crucial for grid management, energy planning, and renewable energy integration.

##  Problem Statement

Energy grid operators face significant challenges in balancing electricity supply and demand. With the increasing integration of renewable energy sources like solar power, accurate forecasting becomes even more critical because:

- **Solar generation is intermittent** - it depends on weather conditions and time of day
- **Load demand fluctuates** - consumption patterns vary throughout the day and across seasons
- **Grid stability requires balance** - supply must match demand in real-time to prevent blackouts or waste

The ability to accurately predict both load demand and solar generation  helps utilities:
- Optimize energy storage and distribution
- Reduce reliance on fossil fuel backup generators
- Lower operational costs
- Improve grid reliability and sustainability

##  Dataset Description

**Source**: Italian energy grid data from 2016

**Key Variables**:
- `utc_timestamp` - Date and time of each observation
- `IT_load_new` - Electrical load/demand in Italy (MW)
- `IT_solar_generation` - Solar power generation in Italy (MW)

**Temporal Resolution**: Hourly data points throughout the year 2016

**Data Characteristics**:
- **Load patterns**: Shows cyclical daily patterns with peaks during business hours and lower demand at night
- **Solar patterns**: Clear diurnal cycle with generation during daylight hours and zero generation at night
- **Seasonal variations**: Both series exhibit seasonal fluctuations throughout the year

##  What We Did

### 1. Data Exploration and Visualization

We started by visualizing the time series data to understand the underlying patterns:

- **Load Analysis**: Identified cyclical patterns corresponding to daily electricity consumption habits (peaks during day, lows at night)
- **Solar Generation Analysis**: Observed expected diurnal patterns with no generation at night and variable daytime generation based on seasonal sunlight availability

### 2. Data Preprocessing

- **Missing Value Handling**: Detected and filled missing values using forward fill method to maintain temporal continuity
- **Data Type Conversion**: Converted timestamp column to proper datetime format for time series analysis

### 3. Stationarity Testing

Before applying ARIMA models, we tested whether the data was stationary (constant mean, variance, and autocorrelation over time):

- **Method**: Augmented Dickey-Fuller (ADF) test
- **Null Hypothesis**: The time series is non-stationary
- **Significance Level**: 0.05

**Results**:
-  **IT_load_new**: p-value << 0.05 → Stationary (no differencing needed)
-  **IT_solar_generation**: p-value << 0.05 → Stationary (no differencing needed)

### 4. Model Parameter Selection

We used ACF (Autocorrelation Function) and PACF (Partial Autocorrelation Function) plots to determine optimal ARIMA parameters:

**ARIMA Model Parameters (p, d, q)**:
- **p**: Number of autoregressive terms (lag observations)
- **d**: Degree of differencing (0 since data is already stationary)
- **q**: Number of moving average terms

**Parameter Selection Criteria**:
- ACF showed gradual decrease
- PACF showed sharp drop after lag 2
- **Selected**: p=2, d=0, q=2 for both models

### 5. Model Training and Evaluation

**Train-Test Split**: 80% training data, 20% testing data

We experimented with multiple ARIMA configurations:
- ARIMA(2,0,2) - baseline model
- ARIMA(2,1,2) - with first-order differencing
- ARIMA(2,2,2) - with second-order differencing

**Evaluation Metric**: Root Mean Squared Error (RMSE) on test set

### 6. Forecasting and Validation

Generated predictions on the test set and compared them against actual values to assess model performance.

## Results

### IT_load_new (Electrical Load) Model

- **Best Model**: ARIMA(2,0,2)
- **RMSE**: ~7,715 MW
- **Performance**: The model successfully captures the general cyclical pattern and structure of electrical load demand
- **Observations**: Some discrepancies between predicted and actual values due to inherent randomness, external factors, and model limitations

### IT_solar_generation (Solar Power) Model

- **Best Model**: ARIMA(2,0,2)
- **RMSE**: ~2,486 MW
- **Performance**: The model effectively captures the diurnal solar generation patterns
- **Observations**: Predictions align well with the overall trend, though some variations exist

### Key Insights

1. **Both series are stationary** - making them suitable for ARIMA modeling without complex transformations
2. **ARIMA captures patterns effectively** - the models successfully identified and forecasted the underlying cyclical behaviors
3. **Room for improvement** - more sophisticated models (SARIMA for seasonality, LSTM neural networks, or ensemble methods) could potentially improve accuracy
4. **Practical applicability** - these forecasts can inform grid operators about expected supply and demand several hours ahead

## Methodology Summary

1. **Data Loading** → Load and inspect the time series dataset
2. **Visualization** → Plot data to identify patterns and anomalies
3. **Preprocessing** → Handle missing values and format data
4. **Stationarity Check** → Perform ADF test to ensure data meets ARIMA requirements
5. **Parameter Tuning** → Use ACF/PACF plots to select optimal p and q values
6. **Model Training** → Fit ARIMA models on training data
7. **Prediction** → Generate forecasts on test set
8. **Evaluation** → Calculate RMSE and visualize actual vs predicted values

## Potential Improvements

- **Seasonal ARIMA (SARIMA)**: Account for seasonal patterns explicitly
- **Exogenous Variables**: Include weather data, holidays, or economic indicators
- **Deep Learning Models**: Explore LSTM or GRU networks for capturing complex temporal dependencies
- **Ensemble Methods**: Combine multiple models for more robust predictions
- **Feature Engineering**: Create lag features, rolling statistics, or calendar-based features
- **Longer Forecasting Horizons**: Extend predictions beyond immediate time steps

## Technologies Used

- **Python** - Programming language
- **Pandas** - Data manipulation and analysis
- **NumPy** - Numerical computations
- **Matplotlib** - Data visualization
- **Statsmodels** - Time series analysis and ARIMA modeling
- **Scikit-learn** - Model evaluation metrics

## Conclusion

This project demonstrates a complete time series forecasting workflow using ARIMA models on real-world energy data. The models successfully capture the underlying patterns in both electrical load demand and solar generation, providing valuable insights for energy grid management. While ARIMA provides a solid baseline, the analysis reveals opportunities for further improvement through more advanced modeling techniques.

The forecasting framework developed here can be adapted for various time series problems including stock price prediction, weather forecasting, sales forecasting, and more.

## 📝 License

This project is available for educational and research purposes.

---

**Author**: Amirtha Ganesh R
**Date**: 2025
### Thanks to my guide who helped me in this project Satyajit Pattnaik !. 
