# Forecast Explainability<a name="forecast-explainability"></a>

**Note**  
Forecast Explainability is only available for Forecasts generated from an AutoPredictor\. You can upgrade existing legacy predictors to AutoPredictor\. See [Upgrading to AutoPredictor](howitworks-predictor.md#upgrading-autopredictor)\.

Forecast Explainability helps you better understand how the attributes in your datasets impact forecasts for specific time series \(item and dimension combinations\) and time points\. Forecast uses a metric called Impact scores to quantify the relative impact of each attribute and determine whether they increase or decrease forecast values\.

For example, consider a forecasting scenario where the target is `sales` and there are two related attributes: `price` and `color`\. Forecast may find that the item’s color has a high impact on sales for certain items, but a negligible effect for other items\. It may also find that a promotion in the summer has a high impact on sales, but a promotion in the winter has little effect\.

To enable Forecast Explainability, your predictor must include at least one of the following: related time series, item metadata, or additional datasets like Holidays and the Weather Index\.

To view aggregated Impact scores for all time series and time points in your datasets, use Predictor Explainability instead of Forecast Explainability\. See [Predictor Explainability](predictor-explainability.md)\.

**Python notebooks**  
For a step\-by\-step guide on Forecast Explainability, see [Item\-Level Explainability](https://github.com/aws-samples/amazon-forecast-samples/blob/main/notebooks/advanced/Item_Level_Explainability/Item_Level_Explanability.ipynb)\.

**Topics**
+ [Interpreting Impact Scores](#forecast-explainability-impact-scores)
+ [Creating Forecast Explainability](#creating-forecast-explainability)
+ [Visualizing Forecast Explainability](#visualizing-forecast-explainability)
+ [Exporting Forecast Explainability](#exporting-forecast-explainability)
+ [Restrictions and best practices](#forecast-explainability-best-practices)

## Interpreting Impact Scores<a name="forecast-explainability-impact-scores"></a>

Impact scores measure the relative impact attributes have on forecast values\. For example, if the ‘price’ attribute has an impact score that is twice as large as the ‘store location’ attribute, you can conclude that the price of an item has twice the impact on forecast values than the store location\.

Impact scores also provide information on whether attributes increase or decrease forecast values\. In the console, this is denoted by the two graphs\. Attributes with blue bars increase forecast values, while attributes with red bars decrease forecast values\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/quicksightwithfilters.png)

It is important to note that Impact scores measure the relative impact of attributes, not the absolute impact\. Therefore, Impact scores cannot be used to determine whether particular attributes improve model accuracy\. If an attribute has a low Impact score, that does not necessarily mean that it has a low impact on forecast values; it means that it has a lower impact on forecast values than other attributes used by the predictor\.

For Forecast Explainability, Impact scores come in two forms: Normalized impact scores and Raw impact scores\. Raw impact scores are based on Shapley values and are not scaled or bounded\. Normalized impact scores scale the raw scores to a value between \-1 and 1\.

Raw impact scores are useful for combining and comparing scores across different Explainability resources\. For example, if your predictor contains over 50 time series or over 500 time points, you can create multiple Forecast Explainability resources to cover a greater combined number of time series or time points, and directly compare raw impact scores for attributes\. However, raw impact scores for Forecast Explainability resources from different forecasts are not directly comparable\.

When viewing Impact scores in the console, you will only see Normalized impact scores\. Exporting Explainability will provide you with both raw and normalized scores\.

## Creating Forecast Explainability<a name="creating-forecast-explainability"></a>

With Forecast Explainability, you can explore how attributes are impacting forecast values for specific time series at specific time points\. After specifying time series and time points, Amazon Forecast calculates Impact scores for only those specific time series and time points\.

You can enable Forecast Explainability for a predictor using the Software Development Kit \(SDK\) or the Amazon Forecast console\. When using the SDK, use the [CreateExplainability](API_CreateExplainability.md) operation\.

**Topics**
+ [Specifying time series](#forecast-explainability-time-series)
+ [Specifying time points](#forecast-explainability-time-points)

### Specifying time series<a name="forecast-explainability-time-series"></a>

**Note**  
A time series is a combination of the item \(item\_id\) and all dimensions in your datasets

When you specify time series \(item and dimension combinations\) for Forecast Explainability, Amazon Forecast calculates Impact scores for attributes for only those specific time series\.

To specify a list of time series, upload a CSV file identifying the time series by their item\_id and dimension values to an S3 bucket\. You can specify up to 50 time series\. You must also define the attributes and attribute types of the time series in a schema\.

For example, a retailer may want to know how a promotion impacts sales for a specific item \(`item_id`\) at a specific store location \(`store_location`\)\. In this use case, you would specify the time series that is the combination of item\_id and store\_location\. 

The following CSV file selects the following five time series:

1. Item\_id: 001, store\_location: Seattle

1. Item\_id: 001, store\_location: New York

1. Item\_id: 002, store\_location: Seattle

1. Item\_id: 002, store\_location: New York

1. Item\_id: 003, store\_location: Denver

```
001, Seattle
001, New York
002, Seattle
002, Seattle
003, Denver
```

The schema defines the first column as `item_id` and the second column as `store_location`\.

You can specify time series using the Forecast console or the Forecast Software Development Kit \(SDK\)\.

------
#### [ Console ]

**To specify time series for Forecast Explainability**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From **Dataset groups**, choose your dataset group\.

1. In the navigation pane, choose **Insights**\.

1. Choose **Create Explainability**\.

1. In the **Explainability name** field, provide a unique name for the Forecast Explainability\.

1. In the **Select forecast** field, choose your forecast\.

1. In the **S3 location** field, enter the location of the CSV file with your time series\.

1. In the **Data schema** field, set the **attribute name** and **attribute type** of the item ID and dimensions used in your time series\.

1. Choose **Create Explainability\.**

------
#### [ SDK ]

**To specify time series for Forecast Explainability**

Using the [CreateExplainability](API_CreateExplainability.md) operation, provide a unique name for ExplainabilityName and provide your forecast ARN for ResourceArn\.

Configure the following datatypes:
+ `ExplainabilityConfig` \- set values for TimeSeriesGranularity to “SPECIFIC” and TimePointGranularity to “ALL”\. \(To specify time points, set TimePointGranularity to “SPECIFIC”\. See [Specifying time points](#forecast-explainability-time-points)\)
+ `S3Config` \- set the values for “Path” to the S3 location of the CSV file and “RoleArn” to a role with access to the S3 bucket\.
+ `Schema` \- define the “AttributeName” and “AttributeType” for item\_id and the dimensions in your time series\.

The example below shows a schema for time series using a combination of “item\_id” and the “store\_location” dimension\. 

```
{
    "ExplainabilityName" : [unique_name],
    "ResourceArn" : [forecast_arn],
    "ExplainabilityConfig" {
        "TimeSeriesGranularity": "SPECIFIC",
        "TimePointGranularity": "ALL"
    },
    "DataSource": {
         "S3Config": {   
            "Path": [S3_path_to_CSV_file],          
            "RoleArn":[role-to-access-s3-bucket]
         }
      },
    "Schema": {
         "Attributes": [ 
            { 
               "AttributeName": "item_id",
               "AttributeType": "string"
            },
                        { 
               "AttributeName": "store_location",
               "AttributeType": "string"
            }
         ]
      },
}
```

------

### Specifying time points<a name="forecast-explainability-time-points"></a>

**Note**  
If you do not specify time points \(`"TimePointGranularity": "ALL"`\), Amazon Forecast will consider the entire forecast horizon when calculating Impact scores\.

When you specify time points for Forecast Explainability, Amazon Forecast calculates Impact scores for attributes for that specific time range\. You can specify up to 500 consecutive time points within the forecast horizon\.

For example, a retailer may want to know how their attributes impact sales during the winter\. In this use case, they would specify the time points to span only the winter period in the forecast horizon\.

You can specify time points using the Forecast console or the Forecast Software Development Kit \(SDK\)\.

------
#### [ Console ]

**To specify time series for Forecast Explainability**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From **Dataset groups**, choose your dataset group\.

1. In the navigation pane, choose **Insights**\.

1. Choose **Create Explainability**\.

1. In the **Explainability name** field, provide a unique name for the Forecast Explainability\.

1. In the **Select forecast** field, choose your forecast\.

1. In the **S3 location** field, enter the location of the CSV file with your time series\.

1. In the **Data schema** field, set the *attribute name* an *attribute type *of the item ID and dimensions used in your time series\.

1. In the **Time duration** field, specify the start date and end date within the calendar\.

1. Choose **Create Explainability\.**

------
#### [ SDK ]

**To specify time series for Forecast Explainability**

Using the [CreateExplainability](API_CreateExplainability.md) operation, provide a unique name for ExplainabilityName and provide your forecast ARN for ResourceArn\. Set the start date \(`StartDateTime`\) and end date \(`EndDateTime`\) using the following timestamp format: `yyyy-MM-ddTHH:mm:ss` \(example: 2015\-01\-01T20:00:00\)\. 

Configure the following datatypes:
+ `ExplainabilityConfig` \- set values for TimeSeriesGranularity to “SPECIFIC” and TimePointGranularity to “SPECIFIC”\.
+ `S3Config` \- set the values for “Path” to the S3 location of the CSV file and “RoleArn” to a role with access to the S3 bucket\.
+ `Schema` \- define the “AttributeName” and “AttributeType” for item\_id and the dimensions in your time series\.

The example below shows a schema for time series using a combination of “item\_id” and the “store\_location” dimension\. 

```
{
    "ExplainabilityName" : [unique_name],
    "ResourceArn" : [forecast_arn],
    "ExplainabilityConfig" {
        "TimeSeriesGranularity": "SPECIFIC",
        "TimePointGranularity": "SPECIFIC"
    },
    "DataSource": {
         "S3Config": {   
            "Path": [S3_path_to_CSV_file],          
            "RoleArn":[role-to-access-s3-bucket]
         }
      },
    "Schema": {
         "Attributes": [ 
            { 
               "AttributeName": "item_id",
               "AttributeType": "string"
            },
                        { 
               "AttributeName": "store_location",
               "AttributeType": "string"
            }
         ]
      },
    "StartDateTime": "string",
    "EndDateTime": "string",
}
```

------

## Visualizing Forecast Explainability<a name="visualizing-forecast-explainability"></a>

When creating Forecast Explainability in the console, Forecast automatically visualizes your Impact scores\. When creating Forecast Explainability with the [CreateExplainability](API_CreateExplainability.md) operation, set `EnableVisualization` to "true" and impact scores for that Explainability resource will be visualized within the console\.

Impact score visualizations last for 30 days from the date of Explainability creation\. To recreate the visualization, create a new Forecast Explainability\.

## Exporting Forecast Explainability<a name="exporting-forecast-explainability"></a>

**Note**  
Export files can directly return information from the Dataset Import\. This makes the files vulnerable to CSV injection if the imported data contains formulas or commands\. For this reason, exported files can prompt security warnings\. To avoid malicious activity, disable links and macros when reading exported files\.

Forecast enables you to export a CSV file of Impact scores to an S3 location\.

The export contains raw and normalized impact scores for the specified time series, as well as normalized aggregated impact scores for all specified time series and all specified time points\. If you didn’t specify time points, the impact scores are already aggregated for all time points in your forecast horizon\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/explainability-export.png)

You can export Forecast Explainability using the Amazon Forecast Software Development Kit \(SDK\) and the Amazon Forecast console\.

------
#### [ Console ]

**To export Forecast Explainability**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From **Dataset groups**, choose your dataset group\.

1. In the navigation pane, choose **Insights**\.

1. Select your Explainability\.

1. From the **Actions** drop\-down, choose **Export**\.

1. In the **Export name** field, provide a unique name for the Forecast Explainability export\.

1. In the **S3 explainability export location**field, enter the S3 location to export the CSV file\.

1. In the **IAM Role** field, choose a role with access to the chosen S3 location\.

1. Choose **Create Explainability Export**\.

------
#### [ SDK ]

**To export Forecast Explainability**

Using the [CreateExplainabilityExport](API_CreateExplainabilityExport.md) operation, specify your S3 location and IAM role in the `Destination` object, along with the `ExplainabilityArn` and `ExplainabilityExportName`\.

For example:

```
{
   "Destination": {
      "S3Config": {
         "Path": "s3://bucket/example-path/",
         "RoleArn": "arn:aws:iam::000000000000:role/ExampleRole"
      }
   },
   "ExplainabilityArn": "arn:aws:forecast:region:explainability/example",
   "ExplainabilityName": "Explainability-export-name",
}
```

------

## Restrictions and best practices<a name="forecast-explainability-best-practices"></a>

Consider the following restrictions and best practices when working with Forecast Explainability\.
+ **Forecast Explainability is only available to Forecasts generated from AutoPredictor \- **You cannot enable Forecast Explainability for Forecasts generated from legacy predictors \(AutoML or manual selection\)\. See [Upgrading to AutoPredictor](howitworks-predictor.md#upgrading-autopredictor)\.

  **Explainability requires attributes** \- Your predictor must include at least one of the following: related time series, item metadata, Holidays, or the Weather Index\.
+ **Impact scores of zero denote no impact** \- If an attribute has an impact score of 0, then that attribute has no significant impact on forecast values\. 
+ **Specify a maximum of 50 time series **\- You can specify up to 50 time series per Forecast Explainability\.
+ **Specify a maximum of 500 time points** \- You can specify up to 500 consecutive time points per Forecast Explainability\.
+ **Forecast also calculates some aggregated Impact scores** \- Forecast will also provide aggregated impact scores for the specified time series and time points\.
+ **Create multiple Forecast Explainability resources for a single Forecast** \- If you want impact scores for more than 50 time series or 500 time points, you can create Explainability resources in batches to span a larger range\.
+ **Compare Raw impact scores across different Forecast Explainability resources** \- Raw impact scores can be directly compared across Explainability resources from the same forecast\.
+ **Predictor Explainability visualizations are available for 30 days after creation** \- To view the visualization after 30 days, retrain the predictor\.