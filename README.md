#  Granite Timeseries For Energy Demand Forecasting

This project demonstrates few-shot fine-tuning of the TinyTimeMixer (TTM) model from IBM's Granite-Time Series foundation model family. TTM is a compact, pre-trained model optimized for Multivariate Time-Series Forecasting.
The goal is to forecast energy demand—specifically total load actual and generation solar—using historical consumption data from Spain, incorporating exogenous weather features for improved accuracy.

Model: TinyTimeMixer (TTM) from ibm-granite/granite-timeseries-ttm-r2.
Technique: Few-shot fine-tuning on $\mathbf{5\%}$ of the training data.
Dataset: Hourly energy consumption and weather data for Spain.
Multivariate Input: Forecasts two target variables simultaneously, incorporating 10 exogenous weather features.

Data Preparation
The script combines two datasets: hourly energy consumption and detailed weather features across Spanish cities.
Exogenous Data Processing: Weather data is aggregated by calculating a 24-hour rolling average, followed by the median across all cities, yielding country-level weather forecasts (e.g., temp, pressure, humidity).
Missing Values: Forward fill (ffill) is used to handle missing values in the target series.
Data Splitting: The final dataset is chronologically split:

After fine-tuning, the TimeSeriesForecastingPipeline is used to:
Evaluate: Generate predictions on the held-out $\mathbf{20\%}$ test set, evaluating performance using standard time-series metrics (MSE, RMSE, MAE).
Simulate Real-World Forecast: Use the last 512 historical observations and the known future values of the 10 control (weather) variables to predict the next 96 hours of energy load and solar 
## Data
<img width="1623" height="294" alt="image" src="https://github.com/user-attachments/assets/514be48c-8564-4619-a28b-4630baf7805b" />

## Prediction
<img width="989" height="789" alt="image" src="https://github.com/user-attachments/assets/a49527f3-8ab2-4452-b8ac-5cb8f1ceb8c3" />

## Forecast
<img width="987" height="190" alt="image" src="https://github.com/user-attachments/assets/82b7b5d4-edec-4c63-a472-3659aa787872" />



# Multivariate_TimeSeries_Forecast
This notebooke demonstrates the usage of a pre-trained TinyTimeMixer model for several multivariate time series forecasting tasks. 
In this project I used a pre-trained TinyTimeMixer model for several multivariate time series forecasting tasks.The TTM model can take an input of 512 time points (context_length), and can forecast upto 96 time points (forecast_length) in the future. We will use the pre-trained TTM in two settings:

Zero-shot: The pre-trained TTM will be directly used to evaluate on the test split of the target data. Note that the TTM was NOT pre-trained on the target data.
Few-shot: The pre-trained TTM will be quickly fine-tuned on only 5% of the train split of the target data, and subsequently, evaluated on the test part of the target data.

This project uses the ETTh1 (Electricity Transformer Temperature) dataset, which contains hourly data from two electricity transformers. This is a multivariate time series forecasting task where the goal is to predict several target variables related to oil temperature and load. The dataset is automatically downloaded from its source on GitHub.

After running the script, two main types of output are generated.
<img width="989" height="1989" alt="image" src="https://github.com/user-attachments/assets/4f0d3f04-2da3-4850-8230-3c3f468b08dd" />


First, the console will display the Mean Squared Error (MSE) on the test set for both the zero-shot and the few-shot experiments. This allows for a direct comparison of the model's performance before and after fine-tuning. You would typically see the evaluation loss from the zero-shot test, followed by a different, and usually lower, loss value from the few-shot test.

Second, the script will produce visualizations. These plots, which compare the model's predictions with the actual ground truth for specific samples, will be saved to a designated output directory. These plots provide a qualitative assessment of the forecasting performance
