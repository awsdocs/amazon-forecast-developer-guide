# Using RELATED\_TIME\_SERIES Datasets<a name="related-time-series-datasets"></a>

A RELATED\_TIME\_SERIES dataset includes time\-series data that isn't included in a TARGET\_TIME\_SERIES dataset and might improve the accuracy of your predictor\.

For example, in the demand forecasting domain, a TARGET\_TIME\_SERIES dataset would contain `timestamp` and`item_id` dimensions, while a complimentary RELATED\_TIME\_SERIES dataset also includes the following supplementary features: `item price`, `promotion`, and `weather`\.

A RELATED\_TIME\_SERIES dataset can contain up to 10 forecast dimensions \(the same ones in your TARGET\_TIME\_SERIES dataset\) and up to 13 related time\-series features\.

You can use a RELATED\_TIME\_SERIES dataset only when training a predictor with the [DeepAR\+](aws-forecast-recipe-deeparplus.md), [NPTS](aws-forecast-recipe-npts.md), and [Prophet](aws-forecast-recipe-prophet.md) algorithms\. The R open\-source algorithms \([ARIMA](aws-forecast-recipe-arima.md) and [ETS](aws-forecast-recipe-ets.md)\) don't take data in a RELATED\_TIME\_SERIES dataset into consideration\.

## RELATED\_TIME\_SERIES Dataset Validation<a name="related-time-series-dataset-validation"></a>

A RELATED\_TIME\_SERIES dataset has the following restrictions:
+ It can't include the target value from the TARGET\_TIME\_SERIES\.
+ It must include `item_id` and `timestamp` dimensions, and at least one related feature \(such as `store` or `location`\)\.
+ RELATED\_TIME\_SERIES feature data must be of the `int` or `float` datatypes\.
+ Data frequency for a RELATED\_TIME\_SERIES dataset must match the TARGET\_TIME\_SERIES data frequency\.

  For example, if the forecast frequency for the TARGET\_TIME\_SERIES dataset is weekly, the data frequency for the RELATED\_TIME\_SERIES must also be weekly even if the TARGET\_TIME\_SERIES data frequency is daily\.
+ The data for each item in the RELATED\_TIME\_SERIES dataset must start on or before the beginning `timestamp` of the corresponding `item_id` in the TARGET\_TIME\_SERIES dataset\.

  For example, if the TARGET\_TIME\_SERIES data for `socks` starts at 2019\-01\-01 and the TARGET\_TIME\_SERIES data for `shoes` starts at 2019\-02\-01, the RELATED\_TIME\_SERIES data for `socks` must begin on or before 2019\-01\-01 and the data for `shoes` must begin on or before 2019\-02\-01\.
+ The last timestamp for every item in the RELATED\_TIME\_SERIES dataset must be on or after the last timestamp in the TARGET\_TIME\_SERIES *plus* the user\-designated forecast window \(called the *forecast horizon*\)\.

  In the example RELATED\_TIME\_SERIES file below, the `timestamp` data for both socks and shoes must end on or after 2019\-07\-01 \(the last recorded timestamp\) *plus* the forecast horizon\. If data frequency in the TARGET\_TIME\_SERIES is daily and the forecast horizon is 10 days, daily data points must be provided in the RELATED\_TIME\_SERIES file until 2019\-07\-11\.
+ The Forecast dimensions provided in the RELATED\_TIME\_SERIES dataset must be either equal to or a subset of the dimensions designated in the TARGET\_TIME\_SERIES dataset\.

**Important**  
Forecast doesn't support aggregations or filling missing values for RELATED\_TIME\_SERIES datasets as it does for TARGET\_TIME\_SERIES datasets\.

## Example: RELATED\_TIME\_SERIES File<a name="related-time-series-example"></a>

The following table shows a correctly configured RELATED\_TIME\_SERIES dataset file\. For this example, assume the following:
+ The last data point was recorded in the TARGET\_TIME\_SERIES dataset on 2019\-07\-01\.
+  The forecast horizon is 10 days\. 
+ The forecast frequency is daily \(`D`\)\. 

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

The following table shows compatible TARGET\_TIME\_SERIES and RELATED\_TIME\_SERIES frequencies for forecasting over the period of a week \(the forecast *granularity*\)\. Because data in a RELATED\_TIME\_SERIES dataset can't be aggregated, Forecast accepts only a RELATED\_TIME\_SEQUENCE data frequency that is the same as the chosen forecasting granularity\.


| Target Input Data Frequency | Related Time Series Frequency | Forecasting Granularity | Supported by Forecast? | 
| --- | --- | --- | --- | 
| Daily | Weekly | Weekly | Yes | 
| Weekly | Weekly | Weekly | Yes | 
| N/A | Weekly | Weekly | Yes | 
| Daily | Daily | Weekly | No | 

## More Info<a name="related-time-series-see-also"></a>
+ Step 2c: Creating a Related Dataset in [Amazon Forecast: predicting time\-series at scale](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/6.Incorporating_Related_Time_Series_dataset_to_your_Predictor.ipynb) in the Amazon Forecast GitHub repository\.