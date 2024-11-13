### Report on Web Traffic Forecasting

#### Authors: 
- Himanshu (MDS202327)
- Eada Surya Deva (MDS202323)

#### Objective:
The project aims to forecast web traffic by analyzing time-series data, identifying patterns such as seasonality, and building suitable forecasting models.

### Data Overview
The data for this analysis originates from the [Kaggle Web Traffic Time Series Forecasting competition](https://www.kaggle.com/competitions/web-traffic-time-series-forecasting). The dataset includes timestamped web traffic counts, which serve as the basis for exploring seasonality and trends in order to build accurate forecasting models.

### Analytical Approach

1. **Stationarity Check**:
   - **ADF Test**: The Augmented Dickey-Fuller (ADF) test was employed to check stationarity.
     - Initial test results indicated non-stationarity with a p-value of 0.034.
     - After first-order differencing, the series became stationary (p-value of 1.5e-07).
   - **Conclusion**: Differencing stabilized the mean and variance across the series.

2. **Seasonality Detection**:
   - **Spectral Plot (FFT)**: Fast Fourier Transform (FFT) identified seasonal cycles of 181 and 7 days.
   - **Differencing Adjustment**: Post differencing, key cycles observed were 7 and 3.5 days, suggesting that seasonality is mainly weekly.
   - **Sub-series Plot**: Confirmed a 7-day seasonal pattern, aligning with weekly trends.

3. **Data Decomposition**:
   - A period of 7 days was selected to decompose the data into trend, seasonality, and residual components, which reinforced the weekly seasonality.

4. **Autocorrelation and Partial Autocorrelation Analysis**:
   - **ACF and PACF Plots**: The ACF plot displayed alternating spikes every 7 lags, affirming a seasonal impact.
   - Post-differencing, the ACF indicated an exponential decay with a damped sinusoidal pattern, hinting that an AR model with a higher order might be suitable.

### Model Selection
Several models were considered to best capture the series' dynamics:

   - **ARIMA**:
     - Models such as ARIMA (1,1,0), ARIMA (7,1,0), and ARIMA (8,1,0) were explored.
   - **SARIMA**:
     - The SARIMA (1,1,0)(7,0,0,7) model was proposed to account for seasonality at 7-day intervals.

### Forecasting and Model Diagnostics
- **ARIMA**:
   - Forecasting with ARIMA yielded an RMSE of 305.5.
- **SARIMA**:
   - SARIMA reduced the RMSE significantly to 153.6, showing a better fit for the seasonal data.
- **Holt’s Winter Method (Triple Exponential Smoothing)**:
   - This model achieved an RMSE of 154.6, indicating competitive performance for seasonal patterns.
- **LSTM Model**:
   - The architecture consisted of two LSTM layers with a final dense layer for output, yielding the lowest RMSE at 66.9, suggesting LSTM’s efficacy in handling complex dependencies.

### Results Summary
| Model                           | RMSE   |
|---------------------------------|--------|
| LSTM                            | 66.9   |
| Holt’s Winter (3x Exponential)  | 154.6  |
| SARIMA (1,1,0)(7,0,0,7)         | 153.6  |
| ARIMA (7,1,0)                   | 305.5  |

### Conclusion
The LSTM model outperformed traditional time series models, highlighting deep learning’s potential in capturing intricate temporal patterns. SARIMA and Holt’s Winter models demonstrated effective handling of seasonality, while ARIMA models were less effective.

### References
- Project resources: [GitHub repository](https://github.com/waitasecant/tsa)
- For further statistical methods: [NIST Statistical Handbook](https://www.itl.nist.gov/div898/handbook/pmc/section4/pmc4462.htm)

### Acknowledgment
This study provides valuable insights into time series forecasting techniques, particularly for web traffic data, by combining classical methods with modern machine learning approaches.
