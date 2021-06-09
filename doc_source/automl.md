# Amazon Forecast AutoML<a name="automl"></a>

When you create a predictor, you can either choose AutoML to let Amazon Forecast optimize the predictor for you, or you can manually choose a Forecast algorithm for your predictor\. When you use AutoML, Forecast trains different models with your target time series, related time series, and item metadata\. It then uses the model with the best accuracy metrics\. 

By default, Forecast evaluates predictors by averaging the [Weighted Quantile Losses](metrics.md#metrics-wQL) \(wQL\) of the 0\.1 \(P10\), 0\.5 \(P50\), and 0\.9 \(P90\) quantiles\. If you specify custom [Forecast Types](metrics.md#forecast-types), Forecast uses the average wQL of those forecast types\. If you are using multiple backtest windows, Forecast uses the averages across all [backtest windows](metrics.md#backtesting)\.

Unless you are certain that you want to use a specific algorithm to train a predictor, we recommend that you use AutoML, which is more versatile and generally results in a more accurate predictor\.

**Topics**
+ [Using AutoML](#using-automl)
+ [Choosing an AutoML strategy](#automl-strategies)
+ [Using Hyperparameter optimization \(HPO\)](#AutoML-HPO)

## Using AutoML<a name="using-automl"></a>

AutoML is valid for all datasets and never causes a predictor training job to fail unnecessarily\. Amazon Forecast applies algorithms and built\-in featurizations like the [Weather Index](weather.md) and [Holidays](holidays.md) only if they comply with your datasets\. For example, Forecast doesn't incorporate the Weather Index into your predictor if your datasets don't contain required attributes like geolocation\.

You can activate AutoML using the Software Development Kit \(SDK\) or the Amazon Forecast console\.

------
#### [ Console ]

**To use AutoML**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From **Dataset groups**, choose your dataset group\.

1. In the navigation pane, choose **Predictors**\.

1. Choose **Train new predictor**\.

1. In the **Predictor details** section, choose **Automatic \(AutoML\)**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/automl-console.PNG)

------
#### [ SDK ]

**To use AutoML**

Using the [CreatePredictor](API_CreatePredictor.md) operation, set the value of `PerformAutoML` to `"true"`\.

```
{
    ...
    "PerformAutoML": "true",
}
```

If you use AutoML, you cannot set a value for the following [CreatePredictor](API_CreatePredictor.md) parameters: 
+ `AlgorithmArn`
+ `HPOConfig`
+ `TrainingParameters`

------

## Choosing an AutoML strategy<a name="automl-strategies"></a>

 By default, AutoML trains a model with each Amazon Forecast algorithm and chooses the one with the best accuracy metrics\. You can override the default strategy that AutoML uses when training a predictor and choose the following alternate optimization strategy:
+ **Optimize for speed**: AutoML prioritizes minimizing latency when training a predictor\. This strategy generally reduces training times and is particularly effective with large, complex datasets\.

The “Optimize for speed” strategy will only return accuracy metrics for the optimized predictor, while the default strategy returns accuracy metrics for all evaluated algorithms\. For all AutoML strategies, you can only export predictor backtest results for the optimized model\.

You can override the default AutoML strategy using the Software Development Kit \(SDK\) or the Amazon Forecast console\.

------
#### [ Console ]

**To use the "Optimize for speed" AutoML strategy**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From **Dataset groups**, choose your dataset group\.

1. In the navigation pane, choose **Predictors**\.

1. Choose **Train new predictor**\.

1. In the **Predictor details** section, choose **Automatic \(AutoML\)**\.

1. In the **AutoML optimization strategy** section, choose **Optimize for speed**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/automl-latency-console.PNG)

------
#### [ SDK ]

**To use the "Optimize for speed" AutoML strategy**

Using the [CreatePredictor](API_CreatePredictor.md) operation, set the value of `PerformAutoML` to `"true"` and `AutoMLOverrideStrategy` to `"LatencyOptimized"`\.

```
{
    ...
    "PerformAutoML": "true",
    "AutoMLOverrideStrategy": "LatencyOptimized",
}
```

If you create a predictor with the `LatencyOptimized` strategy, [DescribePredictor](API_DescribePredictor.md) doesn't return values for the following parameters: 
+ `TrainingParameters`
+ `PredictorExecutionDetails`
+ `AutoMLAlgorithmArns`

------

## Using Hyperparameter optimization \(HPO\)<a name="AutoML-HPO"></a>

Amazon Forecast activates hyperparameter optimization \(HPO\) only when you use the default AutoML strategy\. For the “Optimize for speed” strategy, Forecast minimizes runtime by using the default hyperparameter values during AutoML\.

With the default AutoML strategy, Forecast uses the average Weighted Quantile Loss \(wQL\) of the forecast Ttpes to determine the optimal hyperparameter values\. It uses the `0.1` \(P10\), `0.5` \(P50\), and `0.9` \(P90\) quantiles as the default forecast types\. If you specify custom forecast types when creating a predictor, Forecast evaluates metrics at those specified types\. Forecast uses the first backtest window to find the optimal hyperparameter values\.