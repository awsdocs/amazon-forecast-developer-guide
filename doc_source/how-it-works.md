# How Amazon Forecast Works<a name="how-it-works"></a>

When creating forecasting projects in Amazon Forecast, you work with the following resources:
+ ** [Importing Datasets](howitworks-datasets-groups.md) ** – *Datasets* are collections of your input data\. Dataset groups are collections of datasets that contain complimentary information\. Forecast algorithms use your dataset groups to train custom forecasting models, called predictors\.
+ ** [Training Predictors](howitworks-predictor.md) ** – *Predictors* are custom models trained on your data\. You can train a predictor by choosing a prebuilt algorithm,or by choosing the AutoML option to have Amazon Forecast pick the best algorithm for you\.
+ ** [Generating Forecasts](howitworks-forecast.md) ** – You can generate forecasts for your time\-series data, query them using the [QueryForecast](https://docs.aws.amazon.com/forecast/latest/dg/API_forecastquery_QueryForecast.html) API, or visualize them in the console\.