# Multivariate_TimeSeries_Forecast
This notebooke demonstrates the usage of a pre-trained TinyTimeMixer model for several multivariate time series forecasting tasks. 
In this project I used a pre-trained TinyTimeMixer model for several multivariate time series forecasting tasks.The TTM model can take an input of 512 time points (context_length), and can forecast upto 96 time points (forecast_length) in the future. We will use the pre-trained TTM in two settings:

Zero-shot: The pre-trained TTM will be directly used to evaluate on the test split of the target data. Note that the TTM was NOT pre-trained on the target data.
Few-shot: The pre-trained TTM will be quickly fine-tuned on only 5% of the train split of the target data, and subsequently, evaluated on the test part of the target data.

This project uses the ETTh1 (Electricity Transformer Temperature) dataset, which contains hourly data from two electricity transformers. This is a multivariate time series forecasting task where the goal is to predict several target variables related to oil temperature and load. The dataset is automatically downloaded from its source on GitHub.

After running the script, two main types of output are generated.

First, the console will display the Mean Squared Error (MSE) on the test set for both the zero-shot and the few-shot experiments. This allows for a direct comparison of the model's performance before and after fine-tuning. You would typically see the evaluation loss from the zero-shot test, followed by a different, and usually lower, loss value from the few-shot test.

Second, the script will produce visualizations. These plots, which compare the model's predictions with the actual ground truth for specific samples, will be saved to a designated output directory. These plots provide a qualitative assessment of the forecasting performance
