# Training Predictors<a name="howitworks-predictor"></a>

A predictor is an Amazon Forecast model that is trained using your target time series, related time series, item metadata, and any additional datasets you include\. You can use predictors to generate forecasts based on your time\-series data\. 

By default, Amazon Forecast creates predictors by applying the optimal combination of algorithms to each time series in your datasets\.

**Topics**
+ [Creating a Predictor](#creating-predictors)
+ [Upgrading to AutoPredictor](#upgrading-autopredictor)
+ [Using additional datasets](#using-additional-datasets)
+ [Working with legacy predictors](#legacy-predictors)
+ [Evaluating Predictor Accuracy](metrics.md)
+ [Retraining Predictors](retrain-predictors.md)
+ [Weather Index](weather.md)
+ [Holidays Featurization](holidays.md)
+ [Predictor Explainability](predictor-explainability.md)
+ [Amazon Forecast Algorithms](aws-forecast-choosing-recipes.md)

## Creating a Predictor<a name="creating-predictors"></a>

Amazon Forecast requires the following inputs to train a predictor:
+ **Dataset group** – A dataset group that must include a target time series dataset\. The target time series dataset includes the target attribute \(`item_id`\) and timestamp attribute, as well as any dimensions\. Related time series and Item metadata is optional\. For more information, see [Importing Datasets](howitworks-datasets-groups.md)\.
+ **Forecast frequency** – The granularity of your forecasts \(hourly, daily, weekly, etc\)\.
+ **Forecast horizon** – The number of time steps being forecasted\.

You can also set values for the following optional inputs:
+ **Forecast dimensions** – Dimensions are optional attributes in your target time series dataset that can be used in combination with the target value \(`item_id`\) to create separate time series\.
+ **Forecast types** – The quantiles used to evaluate your predictor\.
+ **Optimization metric** – The accuracy metric used to optimize your predictor\.
+ **Additional datasets** – Built\-in Amazon Forecast datasets like the Weather Index and Holidays\.

You can create a predictor using the Software Development Kit \(SDK\) or the Amazon Forecast console\.



------
#### [ Console ]

**To create a predictor**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From **Dataset groups**, choose your dataset group\.

1. In the navigation pane, choose **Predictors**\.

1. Choose **Train new predictor**\.

1. Provide values for the following mandatory fields:
   +  **Name** \- a unique predictor name\.
   + **Forecast frequency** \- the granularity of your forecasts\.
   + **Forecast horizon** \- The number of time steps to forecast\.

1. Choose **Start**\.

For information on additional datasets, see [ Weather Index](weather.md) and [Holidays Featurization](holidays.md)\. To learn more about customizing forecast types and optimization metrics, see [Evaluating Predictor Accuracy](metrics.md)\.

------
#### [ SDK ]

**To create a predictor**

Using the [`CreateAutoPredictor`](API_CreateAutoPredictor.md) operation, define the following required parameters in the request below:

```
{
  "PredictorName": "string",
  "ForecastHorizon": 14,
  "ForecastFrequency:": "D",
  "DataConfig": {
      "DatasetGroupArn": "..MyDSG",
  },
}
```

To learn more about customizing forecast types and optimization metrics, see [Evaluating Predictor Accuracy](metrics.md)\.

```
{
  ...
  "ForecastDimensions": [ "string" ],
  "ForecastTypes": [ "string" ],
  "OptimizationMetric": "string",
}
```

The Weather Index and Holidays additional datasets are defined within the `DataConfig` datatype\. For information on additional datasets, see [ Weather Index](weather.md) and [Holidays Featurization](holidays.md)\.

```
{
      ...
      "AdditionalDatasets": [{ 
            "Name": "Holiday",
            "Configuration": {
              "CountryCode": ["US"]
            }
           }, {
             "Name": "Weather"
       }],
}
```

------

## Upgrading to AutoPredictor<a name="upgrading-autopredictor"></a>

**Python notebooks**  
For a step\-by\-step guide on upgrading predictors to AutoPredictor, see [Upgrading a predictor to AutoPredictor](https://github.com/aws-samples/amazon-forecast-samples/blob/main/notebooks/basic/Upgrading_to_AutoPredictor/UpgradeToAutoPredictor.ipynb)\.

Predictors created with AutoML or manual selection \(CreatePredictor\) can be upgraded to an AutoPredictor\. Upgrading an existing to AutoPredictor will transfer all the relevant predictor configuration settings\.

After Upgrading to AutoPredictor, the original predictor will remain active and the upgraded predictor will have a separate Predictor ARN\. This enables you to compare accuracy metrics between the two predictors, and you can still generate forecasts with the original predictor\.

You can upgrade a predictor using the Software Development Kit \(SDK\) or the Amazon Forecast console\.

------
#### [ Console ]

**To upgrade a predictor**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. In the navigation pane, choose **Predictors**\.

1. Choose the predictor to upgrade, and choose **Upgrade**\.

1. Set a unique name for the upgraded predictor\.

1. Choose **Upgrade to AutoPredictor**\.

------
#### [ SDK ]

**To upgrade a predictor**

Using the [`CreateAutoPredictor`](API_CreateAutoPredictor.md) operation, assign the predictor a unique name and set the value of `ReferencePredictorArn` to the predictor you wish to upgrade\.

```
{
  "PredictorName": "UpgradedPredictor",
  "ReferencePredictorArn": "arn:aws:forecast:us-west-2:938097332257:predictor/OriginalPredictor"
}
```

When upgrading a predictor, assign values to only the `PredictorName` and `ReferencePredictorArn` parameters\.

------

## Using additional datasets<a name="using-additional-datasets"></a>

Amazon Forecast can include the Weather Index and Holidays when creating your predictor\. The Weather Index incorporates meteorological information into your model and Holidays incorporates information regarding national holidays\.

The Weather Index requires a ‘geolocation’ attribute in your target time series dataset and information regarding time zones for your timestamps\. For more information, see [ Weather Index](weather.md)\.

Holidays includes holiday information on 66 countries\. For more information, see [Holidays Featurization](holidays.md)\.

## Working with legacy predictors<a name="legacy-predictors"></a>

**Note**  
To upgrade an existing predictor to AutoPredictor, see [Upgrading to AutoPredictor](#upgrading-autopredictor)

AutoPredictor is the default and preferred method to create a predictor with Amazon Forecast\. AutoPredictor creates predictors by applying the optimal combination of algorithms for each time series in your dataset\.

Predictors created with AutoPredictor are generally more accurate than predictors created with AutoML or manual selection\. The Forecast Explainability and predictor retraining features are only available for predictors created with AutoPredictor\.

Amazon Forecast can also create legacy predictors in the following ways:

1. **AutoML** \- Forecast finds the best\-performing algorithm and applies it to your entire dataset\.

1. **Manual selection** \- Manually choose a single algorithm that is applied to your entire dataset\.

You can create a legacy predictor using the Software Development Kit \(SDK\) or the Amazon Forecast console\.

------
#### [ Console ]

**To use AutoML**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From **Dataset groups**, choose your dataset group\.

1. In the navigation pane, choose **Predictors**\.

1. Choose **Train new predictor**\.

1. In the **Predictor configuration** section, unselect **Enable AutoPredictor**\.

1. Expand the **Algorithm selection** drop\-down and choose **Automatic \(AutoML\)**\. 

------
#### [ SDK ]

**To use AutoML**

Using the [`CreatePredictor`](API_CreatePredictor.md) operation, set the value of `PerformAutoML` to `"true"`\.

```
{
    ...
    "PerformAutoML": "true",
}
```

If you use AutoML, you cannot set a value for the following CreatePredictor parameters: `AlgorithmArn`, `HPOConfig`, `TrainingParameters`\.

------