# Choosing an Amazon Forecast Algorithm<a name="aws-forecast-choosing-recipes"></a>

Every Amazon Forecast predictor uses an algorithm to train a model, then uses the model to make a forecast using an input dataset group\. To help you get started, Amazon Forecast provides the following predefined algorithms:
+ [Autoregressive Integrated Moving Average \(ARIMA\) Algorithm](aws-forecast-recipe-arima.md)

  `arn:aws:forecast:::algorithm/ARIMA`
+ [DeepAR\+ Algorithm](aws-forecast-recipe-deeparplus.md)\*

  `arn:aws:forecast:::algorithm/Deep_AR_Plus`
+ [Exponential Smoothing \(ETS\) Algorithm](aws-forecast-recipe-ets.md)

  `arn:aws:forecast:::algorithm/ETS`
+ [Non\-Parametric Time Series \(NPTS\) Algorithm](aws-forecast-recipe-npts.md)

  `arn:aws:forecast:::algorithm/NPTS`
+ [Prophet Algorithm](aws-forecast-recipe-prophet.md)

  `arn:aws:forecast:::algorithm/Prophet`

\* Supports hyperparameter optimization \(HPO\)