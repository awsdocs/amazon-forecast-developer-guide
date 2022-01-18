# Predictor Explainability<a name="predictor-explainability"></a>

**Note**  
Predictor Explainability is only available for predictors created with AutoPredictor\. You can upgrade existing legacy predictors to AutoPredictor\. See [Upgrading to AutoPredictor](howitworks-predictor.md#upgrading-autopredictor)\.

Predictor Explainability helps you better understand how the attributes in your datasets impact your target variable\. Forecast uses a metric called Impact scores to quantify the relative impact of each attribute and determine whether they increase or decrease forecast values\.

For example, consider a forecasting scenario where the target is `sales` and there are two related attributes: `price` and `color`\. Forecast may find that an item’s price significantly impacts sales \(high Impact score\), while the item’s color has a negligible effect \(low Impact score\)\.

To enable Predictor Explainability, your predictor must include at least one of the following: related time series, item metadata, or additional datasets like Holidays and the Weather Index\.

To create Impact scores for specific time series and time points, use Forecast Explainability instead of Predictor Explainability\. See [Forecast Explainability](forecast-explainability.md)\.

**Topics**
+ [Interpreting Impact Scores](#predictor-explainability-impact-scores)
+ [Creating Predictor Explainability](#creating-predictor-explainability)
+ [Exporting Predictor Explainability](#exporting-predictor-explainability)
+ [Restrictions and best practices](#predictor-explainability-best-practices)

## Interpreting Impact Scores<a name="predictor-explainability-impact-scores"></a>

Impact scores measure the relative impact attributes have on forecast values\. For example, if the ‘price’ attribute has an impact score that is twice as large as the ‘store location’ attribute, you can conclude that the price of an item has twice the impact on forecast values than the store location\.

 Impact scores also provide information on whether attributes increase or decrease forecast values\. In the console, this is denoted by the two graphs\. Attributes with blue bars increase forecast values, while attributes with red bars decrease forecast values\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/quicksight-unfiltered.png)

In the console, Impact scores range from 0 to 1, where a score of 0 denotes no impact and a score close to 1 denotes a significant impact\. In the SDKs, Impact scores range from \-1 to 1, where the sign denotes the direction of the impact\.

It is important to note that Impact scores measure the relative impact of attributes, not the absolute impact\. Therefore, Impact scores cannot be used to determine whether particular attributes improve model accuracy\. If an attribute has a low Impact score, that does not necessarily mean that it has a low impact on forecast values; it means that it has a lower impact on forecast values than other attributes used by the predictor\.

## Creating Predictor Explainability<a name="creating-predictor-explainability"></a>

**Note**  
You can create a maximum of one Predictor Explainability per predictor

When you enable Predictor Explainability, Amazon Forecast calculates Impact scores for all attributes in your datasets\. The Impact scores can be interpreted as the impact attributes have on overall forecast values\. You can enable Predictor Explainability when you create a predictor, or you can enable the feature after creating the predictor\.

### Enabling Predictor Explainability for a new predictor<a name="creating-predictor-explainability-new"></a>

Enabling Predictor Explainability when creating a new predictor will create both a Predictor resource and Explainability resource\. You can enable Predictor Explainability for a new predictor using the Software Development Kit \(SDK\) or the Amazon Forecast console\.

------
#### [ Console ]

**To enable Predictor Explainability**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From **Dataset groups**, choose your dataset group\.

1. In the navigation pane, choose **Predictors**\.

1. Choose **Train new predictor**\.

1. In the **Predictor configuration** section, choose **Enable Explainability**\.

1. Provide values for the following mandatory fields:
   + **Name** \- a unique predictor name\.
   + **Forecast frequency** \- the granularity of your forecasts\.
   + **Forecast horizon** \- The number of time steps to forecast\.

1. Choose **Start**

------
#### [ SDK ]

**To enable Predictor Explainability**

Using the [CreateAutoPredictor](API_CreateAutoPredictor.md) operation, define the required parameters and set `EnableExplainability` to `true`\.

For example:

```
{
  "PredictorName": "UniquePredictorName",
  "ForecastHorizon": 14,
  "ForecastFrequency:": "D",
  "EnableExplainability": "true",
  "DataConfig": {
      "DatasetGroupArn": "..MyDSG",
  },
}
```

------

### Enabling Predictor Explainability for an existing predictor<a name="creating-predictor-explainability-old"></a>

Enabling Predictor Explainability for an existing predictor will create a Explainability resource for that resource\. You can only create an Explainability resource for predictors that do not already contain an Explainability resource\. To view Impact scores for an updated dataset, retrain or recreate the predictor with the updated data\.

You can enable Predictor Explainability for a new predictor using the Software Development Kit \(SDK\) or the Amazon Forecast console\.

------
#### [ Console ]

**To enable Predictor Explainability**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From **Dataset groups**, choose your dataset group\.

1. In the navigation pane, choose **Predictors**\.

1. Choose your predictor\.

1. In the **Predictor Explainability** section, choose **Enable Explainability**\.

1. Provide a unique name for the Predictor Explainability\.

1. Choose **Start**

------
#### [ SDK ]

**To enable Predictor Explainability**

Using the [CreateExplainability](API_CreateExplainability.md) operation, provide a unique Explainability name for `ExplainabilityName` and set `ResourceARN` to the ARN of your predictor\.

```
{
   "ExplainabilityName": "string",
   "ResourceArn": "string",
}
```

When creating Predictor Explainability, you can only provide values for the following:
+ `ExplainabilityName`
+ `ResourceARN`
+ `EnableVisualization`
+ `Tags`

Other parameters and data types in [CreateExplainability](API_CreateExplainability.md) are for Forecast Explainability\.

------

## Exporting Predictor Explainability<a name="exporting-predictor-explainability"></a>

**Note**  
Export files can directly return information from the Dataset Import\. This makes the files vulnerable to CSV injection if the imported data contains formulas or commands\. For this reason, exported files can prompt security warnings\. To avoid malicious activity, disable links and macros when reading exported files\.

Forecast enables you to export a CSV file of Impact scores to an S3 location\. The Impact scores range from \-1 to 1, where the sign denotes the direction of the impact\. You can export Impact scores using the Amazon Forecast Software Development Kit \(SDK\) and the Amazon Forecast console\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/explainability-global.png)

------
#### [ Console ]

**To export Predictor Explainability**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From **Dataset groups**, choose your dataset group\.

1. In the navigation pane, choose **Predictors**\.

1. Choose your predictor\.

1. In the **Predictor Explainability** section, choose **Export**\.

1. For the **Export name** field, provide a unique name for the export\.

1. For the **S3 explainability export location** field, provide an S3 location to export the CSV file\.

1. For the **IAM Role** field, provide a role with access to the specified S3 location\.

1. Choose **Create export\.**

------
#### [ SDK ]

**To export Predictor Explainability**

Using the [CreateExplainabilityExport](API_CreateExplainabilityExport.md) operation, specify your S3 location and IAM role in the `Destination` object, along with the `ExplainabilityArn` and `ExplainabilityExportName`\.

```
{
   "Destination": {
      "S3Config": {
         "Path": "s3://bucket/example-path/",
         "RoleArn": "arn:aws:iam::000000000000:role/ExampleRole"
      }
   },
   "ExplainabilityArn": "arn:aws:forecast:region:Explainability/example",
   "ExplainabilityExportName": "Explainability-export-name",
}
```

------

## Restrictions and best practices<a name="predictor-explainability-best-practices"></a>

Consider the following restrictions and best practices when working with Predictor Explainability\.
+ **Predictor Explainability is only available to predictors created with AutoPredictor** \- You cannot enable Explainability for legacy predictors that were created with AutoML or through manual selection\. See [Upgrading to AutoPredictor](howitworks-predictor.md#upgrading-autopredictor)\.
+ **Explainability requires attributes** \- Your predictor must include at least one of the following: related time series, item metadata, Holidays, or the Weather Index\.
+ **Predictors are limited to one Explainability resource** \- You cannot create multiple Explainability resources for a predictor\. If you are interested in Impact scores for an updated dataset, retrain your predictor\.
+ **Impact scores of zero denote no impact**\- If an attribute has an impact score of 0, then that attribute has no significant impact on forecast values\.
+ **Retrying failed Predictor Explainability jobs **\- If Forecast successfully creates a Predictor but the Predictor Explainability job fails, you can retry creating Predictor Explainability in the console or with the CreateExplainability operation\.
+ **You cannot create Impact scores for specific time points and time series **\- To view Impact scores for specific time points and time series, see [Forecast Explainability](forecast-explainability.md)\.
+ **Predictor Explainability visualizations are available for 30 days after creation** \- To view the visualization after 30 days, retrain the predictor\.