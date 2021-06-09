# Guidelines and Quotas<a name="limits"></a>

The following sections contain information about Amazon Forecast guidelines and quotas\.

**Topics**
+ [Supported AWS Regions](#regions)
+ [Compliance](#ompliance)
+ [Service Quotas](#limits-table)

## Supported AWS Regions<a name="regions"></a>

For a list of AWS Regions that support Forecast, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#forecast_region) in the *Amazon Web Services General Reference*\.

## Compliance<a name="ompliance"></a>

For more information about Forecast compliance programs, see [AWS Compliance](https://aws.amazon.com/compliance/), [AWS Compliance Programs](https://aws.amazon.com/compliance/programs/), and [AWS Services in Scope by Compliance Program](https://aws.amazon.com/compliance/services-in-scope)\.

## Service Quotas<a name="limits-table"></a>

**Note**  
To request an increase for adjustable quotas, use the [Service Quotas console](https://console.aws.amazon.com/servicequotas/) and follow the steps in the [Requesting a quota increase](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html) section of the *Service Quotas User Guide*\. 

Forecast has the following service quotas\. 


**Quotas Imposed by the [CreateDatasetImportJob](API_CreateDatasetImportJob.md) API**  

| Resource | Default Quota | Adjustable | 
| --- | --- | --- | 
| Maximum number of files in your Amazon S3 bucket | 10,000 |  No | 
| Maximum cumulative size of all files in your Amazon S3 bucket | 30 GB |  Yes | 
| Maximum number of datasets in a dataset group | 3 \(1 for each type\) |  No | 
| Maximum number of rows in a dataset | 3 billion Note: the quota for the *ap\-south\-1* region is 1 billion\. |  Yes | 
|  Maximum number of columns in a target time series dataset \(required columns \+ additional forecast dimensions\)  | 13 \(3 \+ 10\) |  No | 
|  Maximum number of columns in a related time series dataset \(required columns \+ additional forecast dimensions \+ related features\)  | 25 \(2 \+ 10 \+ 13\) |  No | 
| Maximum number of columns in an item metadata dataset | 10 |  No | 


**Quotas Imposed by the [CreatePredictor](API_CreatePredictor.md) API**  

| Resource | Default Quota | Adjustable | 
| --- | --- | --- | 
| Maximum number of backtest windows \([EvaluationParameters](API_EvaluationParameters.md)\) | 5 |  No | 
|  Maximum number of time series per predictor \(number of items X number of unique values across forecast dimensions in the target time series dataset\)  |  5,000,000 across all target time series items and dimensions\.  Note: the quota for the *ap\-south\-1* region is 1,000,000 \.  If you exceed 100,000 items, Forecast supports yearly, monthly, weekly, and daily frequencies instead of more granular frequencies \(such as hourly\)\.  |  Yes | 
| Maximum forecast horizon | CNN\-QR, DeepAR\+, AutoML: The lesser of 500 data points or 1/3 of the target time series dataset length ETS, NPTS, Prophet, ARIMA: The lesser of 500 data points or the length of the target time series dataset minus one\. |  No | 


**General Resource Quotas**  

| Resource | Default Quota | Adjustable | 
| --- | --- | --- | 
| Maximum parallel running CreateDatasetImportJob tasks | 3 |  Yes | 
| Maximum parallel running CreatePredictor tasks | 3 |  Yes | 
| Maximum parallel running CreatePredictor tasks using AutoML | 3 |  Yes | 
| Maximum parallel running CreatePredictorBacktestExportJob tasks | 3 |  Yes | 
| Maximum parallel running CreateForecast tasks | 3 |  Yes | 
| Maximum parallel running CreateForecastExportJob tasks | 3 |  Yes | 
| Maximum parallel running StopResource tasks per resource type | 3 |  Yes | 
| Maximum number of datasets | 1500 |  Yes | 
| Maximum number of dataset groups | 500 |  Yes | 
| Maximum number of dataset import jobs | 1000 |  Yes | 
| Maximum number of predictors | 500 |  Yes | 
| Maximum number of predictor backtest export jobs | 1000 |  Yes | 
| Maximum number of forecasts |  10  |  Yes | 
| Maximum number of forecast export jobs | 1000 |  Yes | 
| Maximum time for which a forecast can be queried on console or [QueryForecast](API_forecastquery_QueryForecast.md) API | 30 days |  No | 
| Maximum number of tags you can add to a resource | 50 |  No | 
| Maximum parallel running QueryForecast API tasks |  10 forecasts, including 5 created with large datasets \(anything over 20GB or 100,000 items\)\. If you have more than 5 forecasts created with large datasets, `QueryForecast` can access only the 5 most recent large dataset forecasts\.  |  No | 