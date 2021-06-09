# Evaluating Predictor Accuracy<a name="metrics"></a>

Amazon Forecast produces accuracy metrics to evaluate predictors and help you choose which to use to generate forecasts\. Forecast evaluates predictors using Root Mean Square Error \(RMSE\), Weighted Quantile Loss \(wQL\), and Weighted Absolute Percentage Error \(WAPE\) metrics\.

Forecast enables you to evaluate predictors using different forecast types, which can be a set of quantile forecasts and the mean forecast\. The mean forecast provides a point estimate, whereas quantile forecasts typically provide a range of possible outcomes\.

To produce accuracy metrics for predictors, Forecast uses *backtesting*, which is the process of testing a predictor against historical data and comparing forecasted values to actual values\.

**Python notebooks**  
For a step\-by\-step guide on evaluating predictor metrics, see [Computing Metrics Using Item\-level Backtests\.](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/advanced/Item_Level_Accuracy/Item_Level_Accuracy_Using_Bike_Example.ipynb)\.

**Topics**
+ [Choosing Forecast Types](#forecast-types)
+ [Backtesting](#backtesting)
+ [Interpreting Accuracy Metrics](#predictor-metrics)
+ [HPO and AutoML](#HPO-AutoML)

## Choosing Forecast Types<a name="forecast-types"></a>

Amazon Forecast uses forecast types to create predictions and evaluate predictors\. Forecast types come in two forms:
+ **Mean forecast type** \- A forecast using the mean as the expected value\. Typically used as point forecasts for a given time point\.
+ **Quantile forecast type** \- A forecast at a specified quantile\. Typically used to provide a prediction interval, which is a range of possible values to account for forecast uncertainty\. For example, a forecast at the `0.65` quantile will estimate a value that is lower than the observed value 65% of the time\.

By default, Forecast uses the following values for the predictor forecast types: `0.1` \(P10\), `0.5` \(P50\), and `0.9` \(P90\)\. You can choose up to five custom forecast types, including `mean` and quantiles ranging from `0.01` \(P1\) to `0.99` \(P99\)\.

Quantiles can provide an upper and lower bound for forecasts\. For example, using the forecast types `0.1` \(P10\) and `0.9` \(P90\) provides a range of values known as an 80% confidence interval\. The observed value is expected to be lower than the P10 value 10% of the time, and the P90 value is expected to be higher than the observed value 90% of the time\. By generating forecasts at p10 and P90, you can expect the true value to fall between those bounds 80% of the time\. This range of values is depicted by the shaded region between P10 and P90 in the figure below\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/quantiles-intervals.png)

You can also use a quantile forecast as a point forecast when the cost of underpredicting differs from the cost of overpredicting\. For example, in some retail cases the cost of being understocked is higher than the cost of being overstocked\. In these cases, the forecast at 0\.65 \(P65\) is more informative than the median \(P50\) or mean forecast\.

When training a predictor, you can choose custom forecast types using the Amazon Forecast Software Development Kit \(SDK\) and Amazon Forecast console\. 

------
#### [ Forecast SDK ]

Using the [ `CreatePredictor`](API_CreatePredictor.md) operation, specify the custom forecast types in the `ForecastTypes` parameter\. Format the parameter as an array of strings\.

For example, to create a predictor at the `0.01`, `mean`, `0.65`, and `0.99` forecast types, use the following code\.

```
{
    "ForecastTypes": [ "0.01", "mean", "0.65", "0.99" ],
},
```

------
#### [ Forecast Console ]

During the **Train Predictor** stage, specify the custom forecast types in the **Forecast types** field\. Choose **Add new forecast type** and enter a forecast type value\.

 For example, to create a predictor using the `0.01`, `mean`, `0.65`, and `0.99` forecast types, enter the following values in the **Forecast types** fields shown below\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/predictor-custom-quantiles.png)

------

## Backtesting<a name="backtesting"></a>

Amazon Forecast uses backtesting to tune parameters and produce accuracy metrics\. To perform backtesting, Forecast automatically splits your time\-series data into two sets: a training set and a testing set\. The training set is used to train a model and generate forecasts for datapoints within the testing set\. Forecast evaluates the model's accuracy by comparing forecasted values with observed values in the testing set\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/evaluation-offset.png)

Forecast uses backtesting to calculate Root Mean Square Error \(RMSE\), Weighted Quantile Loss \(wQL\), and Weighted Absolute Percentage Error \(WAPE\) metrics\. If you run multiple backtests, Forecast averages each metric over all backtest windows\.

Forecast omits filled values from the backtesting process, and any item with filled values within a given backtest window will be excluded from that backtest\. This is because Forecast only compares forecasted values with observed values during backtesting, and filled values are not observed values\.

### Setting Backtesting Parameters<a name="backtesting-parameters"></a>

By default, Forecast computes one backtest, with the size of the backtest window \(testing set\) equal to the length of the forecast horizon \(prediction window\)\. You can set both the *backtest window length* and the *number of backtest scenarios* when training a predictor\.

The backtest window must be at least as large as the forecast horizon, and smaller than half the length of the entire target time\-series dataset\. You can choose from between 1 and 5 backtests\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/evaluation-backtests.png)

Generally, increasing the number of backtests produces more reliable accuracy metrics, since a larger portion of the time series is used during testing and Forecast is able to take an average of metrics across all backtests\.

You can set the backtesting parameters using the Amazon Forecast Software Development Kit \(SDK\) and the Amazon Forecast console\.

------
#### [ Forecast SDK ]

Using the [CreatePredictor](API_CreatePredictor.md) operation, set the backtest parameters in the [EvaluationParameters](API_EvaluationParameters.md) datatype\. Specify the length of the testing set during backtesting with the `BackTestWindowOffset` parameter, and the number of backtest windows with the `NumberOfBacktestWindows` parameter\.

For example, to run 2 backtests with a testing set of 10 time points, use the follow code\.

```
"EvaluationParameters": {
    "BackTestWindowOffset": 10,
    "NumberOfBacktestWindows": 2
}
```

------
#### [ Forecast Console ]

During the **Train Predictor** stage, set the length of the testing set during backtesting with the **Backtest window offset** field, and the number of backtest windows with the **Number of backtest windows** field\.

For example, to run 2 backtests with a testing set of 10 time points, set the following values\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/predictor-backtest-windows.png)

------

### Exporting Backtest Results<a name="backtest-exports"></a>

**Note**  
For AutoML, Forecast will only export backtest results for the winning algorithm\.

Forecast enables you to export forecasted values and accuracy metrics generated during backtesting\. You can use these exports to evaluate specific items at specific time points and quantiles, and better understand your predictor\. The backtest exports are sent to a specified S3 location and contains two folders:
+ **forecasted\-values**: Contains CSV files with forecasted values at each forecast type for each backtest\.
+ **accuracy\-metrics\-values**: Contains CSV files with metrics for each backtest, along with the average across all backtests\. These metrics include wQL for each quantile, RMSE, and WAPE\.

The `forecasted-values` folder contains forecasted values at each forecast type for each backtest window\. It also includes information on item IDs, dimensions, timestamps, target values, and backtest window start and end times\.

The `accuracy-metrics-values` folder contains accuracy metrics for each backtest window, as well as the average metrics across all backtest windows\. It contains wQL metrics for each specified quantile, as well as RMSE and WAPE metrics\. The export also includes information on item\_ids, dimensions, and backtest window start and end times\. Metrics for individual backtests have a `backtest_window` value of `Computed`, while the backtest averages have a value of `Summary`\. Metrics for items with NaN values are shown as `not defined` in backtest export files\.

Files within both folders follow the naming convention: `<ExportJobName>_<ExportTimestamp>_<PartNumber>.csv`\. 

Below is an example of export files for a predictor trained at the P10, P50, and P90 forecast types\.

------
#### [ forecasted\-values ]

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/export-csv-forecasts.PNG)

------
#### [ accuracy\-metrics\-values ]

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/export-csv-metrics.PNG)

------

You can export backtest results using the Amazon Forecast Software Development Kit \(SDK\) and the Amazon Forecast console\.

------
#### [ Forecast SDK ]

Using the [`CreatePredictorBacktestExportJob`](API_CreatePredictorBacktestExportJob.md) operation, specify your S3 location and IAM role in the [`DataDestination`](API_DataDestination.md) object, along with the `PredictorArn` and `PredictorBacktestExportJobName`\.

For example:

```
{
   "Destination": { 
      "S3Config": { 
         "Path": "s3://bucket/example-path/",
         "RoleArn": "arn:aws:iam::000000000000:role/ExampleRole"
      }
   },
   "PredictorArn": "arn:aws:forecast:region:predictor/example",
   "PredictorBacktestExportJobName": "backtest-export-name",
}
```

------
#### [ Forecast Console ]

Choose your predictor on the **Predictors** page\. In the **Predictor metrics** section, choose **Export backtest results**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/export-backtest-results-button.png)

During the **Create predictor backtest export** stage, set the **Export name**, **IAM Role**, and **S3 predictor backtest export location** fields\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/console-export-screen.PNG)

------

## Interpreting Accuracy Metrics<a name="predictor-metrics"></a>

 Amazon Forecast provides Root Mean Square Error \(RMSE\), Weighted Quantile Loss \(wQL\), and Weighted Absolute Percentage Error \(WAPE\) metrics to evaluate your predictors\. Along with metrics for the overall predictor, Forecast calculates metrics for each backtest window\.

You can view accuracy metrics for your predictors using the Amazon Forecast Software Development Kit \(SDK\) and the Amazon Forecast console\.

------
#### [ Forecast SDK ]

Using the [GetAccuracyMetrics](API_GetAccuracyMetrics.md) Operation, specify your `PredictorArn` to view the RMSE, WAPE, and wQL metrics for each backtest\.

```
{
    "PredictorArn": "arn:aws:forecast:region:acct-id:predictor/example-id"
}
```

------
#### [ Forecast Console ]

Choose your predictor on the **Predictors** page\. Accuracy metrics for the predictor are shown in the **Predictor metrics** section\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/predictor-backtest-output.png)

------

**Note**  
 For wQL, RMSE, and WAPE metrics, a lower value indicates a superior model\. 

**Topics**
+ [Weighted Quantile Loss \(wQL\)](#metrics-wQL)
+ [Weighted Absolute Percentage Error \(WAPE\)](#metrics-WAPE)
+ [Root Mean Square Error \(RMSE\)](#metrics-RMSE)

### Weighted Quantile Loss \(wQL\)<a name="metrics-wQL"></a>

The Weighted Quantile Loss \(wQL\) metric measures the accuracy of a model at a specified quantile\. It is particularly useful when there are different costs for underpredicting and overpredicting\. By setting the weight \(*τ*\) of the wQL function, you can automatically incorporate differing penalties for underpredicting and overpredicting\.

The loss function is calculated as follows\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/metrics-quantile-loss.png)

Where:  
*τ* \- a quantile in the set \{0\.01, 0\.02, \.\.\., 0\.99\}  
qi,t\(τ\) \- the τ\-quantile that the model predicts\.  
yi,t \- the observed value at point \(i,t\)

The quantiles \(τ\) for wQL can range from 0\.01 \(P1\) to 0\.99 \(P99\)\. The wQL metric cannot be calculated for the mean forecast\.

By default, Forecast computes wQL at `0.1` \(P10\), `0.5` \(P50\), and `0.9` \(P90\)\.
+ **P10 \(0\.1\)** \- The true value is expected to be lower than the predicted value 10% of the time\.
+ **P50 \(0\.5\)** \- The true value is expected to be lower than the predicted value 50% of the time\. This is also known as the median forecast\.
+ **P90 \(0\.9\)** \- The true value is expected to be lower than the predicted value 90% of the time\.

In retail, the cost of being understocked is often higher than the cost of being overstocked, and so forecasting at P75 \(*τ* = 0\.75\) can be more informative than forecasting at the median quantile \(P50\)\. In these cases, wQL\[0\.75\] assigns a larger penalty weight to underforecasting \(0\.75\) and a smaller penalty weight to overforecasting \(0\.25\)\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/p50-p75-prediction.jpg)

The figure above shows the differing demand forecasts at wQL\[0\.50\] and wQL\[0\.75\]\. The forecasted value at P75 is significantly higher than the forecasted value at P50 because the P75 forecast is expected to meet demand 75% of the time, whereas the P50 forecast is only expected to meet demand 50% of the time\.

When the sum of observed values over all items and time points is approximately zero in a given backtest window, the weighted quantile loss expression is undefined\. In these cases, Forecast outputs the unweighted quantile loss, which is the numerator in the wQL expression\.

### Weighted Absolute Percentage Error \(WAPE\)<a name="metrics-WAPE"></a>

The Weighted Absolute Percentage Error \(WAPE\) is a commonly used metric to measure model accuracy\. It measures the overall deviation of forecasted values from observed values\. WAPE is always nonnegative, and a lower value indicates a more accurate model\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/WAPE.png)

Where:  
yi,t \- the observed value at point \(i,t\)  
ŷi,t \- the predicted value at point \(i,t\)

 Forecast uses the mean forecast as the predicted value, ŷi,t\. 

WAPE is more robust to outliers than Root Mean Square Error \(RMSE\) because it uses the absolute error instead of the squared error\. For general use cases, it is the more informative metric\.

Amazon Forecast previously referred to the WAPE metric as the Mean Absolute Percentage Error \(MAPE\) and used the median forecast \(P50\) as the predicted value\. Forecast now uses the mean forecast to calculate WAPE\. The wQL\[0\.5\] metric is equivalent to the WAPE\[median\] metric, as shown below:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/wql-to-wape.PNG)

### Root Mean Square Error \(RMSE\)<a name="metrics-RMSE"></a>

Root Mean Square Error \(RMSE\) is a commonly used metric to measure model accuracy\. Like WAPE, it measures the overall deviation of estimates from observed values\. A lower value indicates a more accurate model\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/metrics-rmse.png)

Where:  
yi,t \- the observed value at point \(i,t\)  
ŷi,t \- the predicted value at point \(i,t\)  
nT \- the number of data points in a testing set

Forecast uses the mean forecast as the predicted value, ŷi,t\. When calculating predictor metrics, nT is the number of data points in a backtest window\. 

RMSE uses the squared value of the residuals, which amplifies the impact of outliers\. In use cases where only a few large mispredictions can be very costly, the RMSE is the more relevant metric\. However, WAPE is the more informative metric in general use cases\. 

Predictors created before November 11, 2020 calculated RMSE using the 0\.5 quantile \(P50\) by default\. Forecast now uses the mean forecast\.

## HPO and AutoML<a name="HPO-AutoML"></a>

By default, Amazon Forecast uses the `0.1` \(P10\), `0.5` \(P50\), and `0.9` \(P90\) quantiles for hyperparameter tuning during hyperparameter optimization \(HPO\) and for model selection during AutoML\. If you specify custom forecast types when creating a predictor, Forecast uses those forecast types during HPO and AutoML\. 

If custom forecast types are specified, Forecast evaluates metrics at those specified forecast types, and takes the averages of those metrics to determine the optimal outcomes during HPO and AutoML\.

For both AutoML and HPO, Forecast chooses the option that minimizes the average losses over the forecast types\. During HPO, Forecast uses the first backtest window to find the optimal hyperparameter values\. During AutoML, Forecast uses the averages across all backtest windows and the optimal hyperparameters values from HPO to find the optimal algorithm\.