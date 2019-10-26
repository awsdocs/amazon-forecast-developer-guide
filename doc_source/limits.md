# Guidelines and Limits<a name="limits"></a>

The following sections contain information about Amazon Forecast guidelines and limits\.

**Topics**
+ [Supported AWS Regions](#regions)
+ [Compliance](#ompliance)
+ [Service Limits](#limits-table)

## Supported AWS Regions<a name="regions"></a>

For a list of AWS Regions that support Forecast, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#forecast_region) in the *Amazon Web Services General Reference*\.

## Compliance<a name="ompliance"></a>

For more information about Forecast compliance programs, see [AWS Compliance](https://aws.amazon.com/compliance/), [AWS Compliance Programs](https://aws.amazon.com/compliance/programs/), and [AWS Services in Scope by Compliance Program](https://aws.amazon.com/compliance/services-in-scope)\.

## Service Limits<a name="limits-table"></a>

Forecast has the following service limits\.


**Limits Imposed by the [CreateDatasetImportJob](API_CreateDatasetImportJob.md) API**  

| Resource | Default Limit | 
| --- | --- | 
| Maximum number of files in your Amazon S3 bucket | 10,000 | 
| Maximum cumulative size of all files in your Amazon S3 bucket | 5 GB | 
| Maximum number of datasets in a dataset group | 3 \(1 for each type\) | 
| Maximum number of rows in a dataset | 100 million | 
| Maximum number of columns in a TARGET\_TIME\_SERIES dataset \(required columns \+ additional forecast dimensions\) | 13 \(3 \+ 10\) | 
| Maximum number of columns in a RELATED\_TIME\_SERIES dataset \(required columns \+ additional forecast dimensions \+ related features\) | 25 \(2 \+ 10 \+ 13\) | 
| Maximum number of columns in an ITEM\_METADATA dataset | 10 | 


**Limits Imposed by the [CreatePredictor](API_CreatePredictor.md) API**  

| Resource | Default Limit | 
| --- | --- | 
| Maximum NumberOfBacktestWindows \([EvaluationParameters](API_EvaluationParameters.md)\) | 5 | 
| Maximum number of forecasts per predictor \(number of rows X number of forecast dimensions in the TARGET\_TIME\_SERIES dataset\) | 100,000 across all dimensions | 
| Forecast horizon | The lesser of 500 data points or 1/3 of the TARGET\_TIME\_SERIES dataset length | 


**General Resource Limits**  

| Resource | Default Limit | 
| --- | --- | 
| Maximum parallel running CreateDatasetImportJob tasks | 3 | 
| Maximum parallel running CreatePredictor tasks | 3 | 
| Maximum parallel running [CreateForecast](API_CreateForecast.md) tasks | 3 | 
| Maximum number of dataset import jobs | 1000 | 
| Maximum number of predictors | 500 | 
| Maximum number of forecasts | 10 | 
| Maximum number of forecast export jobs | 1000 | 
| Maximum number of parallel forecast export jobs | 3 | 
| Maximum time for which a forecast can be queried on \(consele or API\) | 30 days | 