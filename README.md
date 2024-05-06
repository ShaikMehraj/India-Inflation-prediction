# India-Inflation-prediction

We are taking data from gov department website namely MoSPI(Minister of Statistics and Programme Implementation).

Data set consists of different metrics and categories like Rural , Urban and Combined .
Annual inflation is consider as combined(rural and urban) General index of CPI.


Every Time series data exhibits trends and seasonal patterns .In this code will understand series if has any linear trends and sequential seasonal patterns by visualizing it .

Non-stationary data has fluctuations and wide spread data points , it is difficult to forecast with such data for more precise inflation rate .  

As per theoretical understanding If the p-value is less than or equal to the significance level (0.05 here) and the ADF statistic is less than the critical value at the chosen significance level, it indicates strong evidence against a unit root (non-stationarity), suggesting the data is stationary.But our series has high P-value so, which indicates it has weak null hypothesis, time series has a unit root, indicating it is non-stationary. 

We perform ACF and PACF plots  (But why…..)
    Analyze the ACF and PACF plots of your original data. These plots can reveal trends or seasonality that might be causing non-stationarity.

Trends:
If the ACF plot shows a slow decline towards zero or the PACF shows a significant non-zero value at lag 1 with subsequent lags decaying slowly, it suggests a trend (linear or non-linear) might be present.

 Seasonal :
If the ACF and PACF plots exhibit spikes at regular intervals corresponding to the seasonal period (e.g., every 12 lags for monthly data), it indicates seasonality is contributing to non-stationarity.

Depending on the trend of data we apply logarithmic transformation (log(x)) or a square root transformation (sqrt(x)) can help stabilize the variance and achieve stationarity.

We also utilize Differencing function to attain stability , depending on performance we may also append function multiple times .

In this Forecast we are facing challenge with less  data and no dependent variable other than time , across all the model SARIMA has best performance with that conditions.

Frist let us understand ARIMA
    A statistical model is autoregressive it predicts future values based on past values. It is mainly composed of three main components which work collectively work to achieve target 

Autoregressive (AR):
    The AR component models the current value of the series as a linear function of a certain number of past values (lags) of the series itself.
It captures the dependence of the current value on its recent history

Integrated (I):

    The I component refers to differencing. If the data has a trend (non-stationary), differencing is applied to remove the trend and make the series stationary.

Moving Average (MA):

The MA component incorporates the error terms (forecasting errors) from past time steps to improve the model's accuracy.
It essentially takes a weighted average of past forecast errors to adjust future forecasts.

Then it arasies a question why we are using SARIMA

Unlike ARIMA (Autoregressive Integrated Moving Average) which focuses on non-seasonal data, SARIMA explicitly considers seasonal patterns in the data. 
SARIMA is a powerful tool for forecasting time series data with seasonal patterns.

As we mentioned above there are 3 major components in ARIMA , likewise we are encompassing 3 more parameter of SARIMA with extra parameter lag (12, 12 months for seasonality).

p (AR order): The number of past values of the series included in the AR model.
d (differencing order): The number of times the data is differenced to achieve stationarity.
q (MA order): The number of past forecast errors included in the MA model.
P (seasonal AR order): Similar to p, but for the seasonal component (e.g., number of past seasonal values).
D (seasonal differencing order): Similar to d, but for the seasonal component (e.g., number of times to difference seasonally).
Q (seasonal MA order): Similar to q, but for the seasonal component (e.g., number of past seasonal forecast errors).
m (seasonality): The number of periods in a single season (e.g., 12 for monthly data).

This is how parameters works 

In AR(2), the model considers the effects of the previous two lags (t-1 and t-2) on the current value (t). 

I(1) indicates that the data has been differenced once to achieve stationarity.

In MA(2), the model considers the effects of the previous two error terms (ε_(t-1) and ε_(t-2)) on the current value.

In SARIMA also has the same functional parameter but with seasonal influence in it.

In this how are we going to know best fitting parameter values for training model ? 

    To tackle this  challenge we are simple iteratively make model learn  with specified range of values , in the out  come we have best combination of value for parameter with lowest AIC and BIC value .
