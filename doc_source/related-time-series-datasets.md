# Using Related Time Series Datasets<a name="related-time-series-datasets"></a>

A related time series dataset includes time\-series data that isn't included in a target time series dataset and might improve the accuracy of your predictor\.

For example, in the demand forecasting domain, a target time series dataset would contain `timestamp` and `item_id` dimensions, while a complimentary related time series dataset also includes the following supplementary features: `item price`, `promotion`, and `weather`\.

A related time series dataset can contain up to 10 forecast dimensions \(the same ones in your target time series dataset\) and up to 13 related time\-series features\.

You can use a related time series dataset only when training a predictor with the [DeepAR\+](aws-forecast-recipe-deeparplus.md) and [Prophet](aws-forecast-recipe-prophet.md) algorithms\. The [NPTS](aws-forecast-recipe-npts.md) algorithm and the R open\-source algorithms \([ARIMA](aws-forecast-recipe-arima.md) and [ETS](aws-forecast-recipe-ets.md)\) don't take data in a related time series dataset into consideration\.

## Related Time Series Dataset Validation<a name="related-time-series-dataset-validation"></a>

A related time series dataset has the following restrictions:
+ It can't include the target value from the target time series\.
+ It must include `item_id` and `timestamp` dimensions, and at least one related feature \(such as `price`\)\.
+ Related time series feature data must be of the `int` or `float` datatypes\.
+ The frequency at which data is recorded in the related time series dataset must match the interval at which you want to generate forecasts \(the forecasting *granularity*\)\.

  For example, if you want to generate forecasts at a weekly granularity, the frequency at which data is recorded in the related time series must also be weekly, even if the frequency at which data is recorded in the target time series is daily\.
+ The data for each item in the related time series dataset must start on or before the beginning `timestamp` of the corresponding `item_id` in the target time series dataset\.

  For example, if the target time series data for `socks` starts at 2019\-01\-01 and the target time series data for `shoes` starts at 2019\-02\-01, the related time series data for `socks` must begin on or before 2019\-01\-01 and the data for `shoes` must begin on or before 2019\-02\-01\.
+ The last timestamp for every item in the related time series dataset must be on or after the last timestamp in the target time series *plus* the user\-designated forecast window \(called the *forecast horizon*\)\.

  In the example related time series file below, the `timestamp` data for both socks and shoes must end on or after 2019\-07\-01 \(the last recorded timestamp\) *plus* the forecast horizon\. If data frequency in the target time series is daily and the forecast horizon is 10 days, daily data points must be provided in the related time series file until 2019\-07\-11\.
+ The Forecast dimensions provided in the related time series dataset must be either equal to or a subset of the dimensions designated in the target time series dataset\.

**Important**  
Forecast doesn't support aggregations or filling missing values for related time series datasets as it does for target time series datasets\.

## Example: Related Time Series File<a name="related-time-series-example"></a>

The following table shows a correctly configured related time series dataset file\. For this example, assume the following:
+ The last data point was recorded in the target time series dataset on 2019\-07\-01\.
+  The forecast horizon is 10 days\. 
+ The forecast granularity is daily \(`D`\)\. 

This means that the user had to include data points up until 2019\-07\-11\. 

A "`…`" row indicates all of the data points in between the previous and succeeding rows\.


| `timestamp` | `item_id` | `store` | `price` | 
| --- | --- | --- | --- | 
| 2019\-01\-01 | socks | NYC | 10 | 
| 2019\-01\-02 | socks | NYC | 10 | 
| 2019\-01\-03 | socks | NYC | 15 | 
| \.\.\. | 
| 2019\-06\-01 | socks | NYC | 10 | 
| \.\.\. | 
| 2019\-07\-01 | socks | NYC | 10 | 
| \.\.\. | 
| 2019\-07\-11 | socks | NYC | 20 | 
| 2019\-01\-05 | socks | SFO | 45 | 
| \.\.\. | 
| 2019\-06\-05 | socks | SFO | 10 | 
| \.\.\. | 
| 2019\-07\-01 | socks | SFO | 10 | 
| \.\.\. | 
| 2019\-07\-11 | socks | SFO | 30 | 
| 2019\-02\-01 | shoes | ORD | 50 | 
| \.\.\. | 
| 2019\-07\-01 | shoes | ORD | 75 | 
| \.\.\. | 
| 2019\-07\-11 | shoes | ORD | 60 | 

## Example: Forecasting Granularity<a name="related-time-series-granularity"></a>

The following table shows compatible data recording frequencies for target time series and related time series to forecast at a weekly granularity\. Because data in a related time series dataset can't be aggregated, Forecast accepts only a related time series data frequency that is the same as the chosen forecasting granularity\.


| Target Input Data Frequency | Related Time Series Frequency | Forecasting Granularity | Supported by Forecast? | 
| --- | --- | --- | --- | 
| Daily | Weekly | Weekly | Yes | 
| Weekly | Weekly | Weekly | Yes | 
| N/A | Weekly | Weekly | Yes | 
| Daily | Daily | Weekly | No | 

## More Info<a name="related-time-series-see-also"></a>
+ Step 2c: Creating a Related Dataset in [Amazon Forecast: predicting time\-series at scale](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/6.Incorporating_Related_Time_Series_dataset_to_your_Predictor.ipynb) in the Amazon Forecast GitHub repository\.