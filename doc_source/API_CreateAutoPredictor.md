# CreateAutoPredictor<a name="API_CreateAutoPredictor"></a>

Creates an Amazon Forecast predictor\.

Amazon Forecast creates predictors with AutoPredictor, which involves applying the optimal combination of algorithms to each time series in your datasets\. You can use [CreateAutoPredictor](#API_CreateAutoPredictor) to create new predictors or upgrade/retrain existing predictors\.

 **Creating new predictors** 

The following parameters are required when creating a new predictor:
+  `PredictorName` \- A unique name for the predictor\.
+  `DatasetGroupArn` \- The ARN of the dataset group used to train the predictor\.
+  `ForecastFrequency` \- The granularity of your forecasts \(hourly, daily, weekly, etc\)\.
+  `ForecastHorizon` \- The number of time\-steps that the model predicts\. The forecast horizon is also called the prediction length\.

When creating a new predictor, do not specify a value for `ReferencePredictorArn`\.

 **Upgrading and retraining predictors** 

The following parameters are required when retraining or upgrading a predictor:
+  `PredictorName` \- A unique name for the predictor\.
+  `ReferencePredictorArn` \- The ARN of the predictor to retrain or upgrade\.

When upgrading or retraining a predictor, only specify values for the `ReferencePredictorArn` and `PredictorName`\. 

## Request Syntax<a name="API_CreateAutoPredictor_RequestSyntax"></a>

```
{
   "DataConfig": { 
      "AdditionalDatasets": [ 
         { 
            "Configuration": { 
               "string" : [ "string" ]
            },
            "Name": "string"
         }
      ],
      "AttributeConfigs": [ 
         { 
            "AttributeName": "string",
            "Transformations": { 
               "string" : "string" 
            }
         }
      ],
      "DatasetGroupArn": "string"
   },
   "EncryptionConfig": { 
      "KMSKeyArn": "string",
      "RoleArn": "string"
   },
   "ExplainPredictor": boolean,
   "ForecastDimensions": [ "string" ],
   "ForecastFrequency": "string",
   "ForecastHorizon": number,
   "ForecastTypes": [ "string" ],
   "OptimizationMetric": "string",
   "PredictorName": "string",
   "ReferencePredictorArn": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateAutoPredictor_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [DataConfig](#API_CreateAutoPredictor_RequestSyntax) **   <a name="forecast-CreateAutoPredictor-request-DataConfig"></a>
The data configuration for your dataset group and any additional datasets\.  
Type: [DataConfig](API_DataConfig.md) object  
Required: No

 ** [EncryptionConfig](#API_CreateAutoPredictor_RequestSyntax) **   <a name="forecast-CreateAutoPredictor-request-EncryptionConfig"></a>
An AWS Key Management Service \(KMS\) key and an AWS Identity and Access Management \(IAM\) role that Amazon Forecast can assume to access the key\. You can specify this optional object in the [CreateDataset](API_CreateDataset.md) and [CreatePredictor](API_CreatePredictor.md) requests\.  
Type: [EncryptionConfig](API_EncryptionConfig.md) object  
Required: No

 ** [ExplainPredictor](#API_CreateAutoPredictor_RequestSyntax) **   <a name="forecast-CreateAutoPredictor-request-ExplainPredictor"></a>
Create an Explainability resource for the predictor\.  
Type: Boolean  
Required: No

 ** [ForecastDimensions](#API_CreateAutoPredictor_RequestSyntax) **   <a name="forecast-CreateAutoPredictor-request-ForecastDimensions"></a>
An array of dimension \(field\) names that specify how to group the generated forecast\.  
For example, if you are generating forecasts for item sales across all your stores, and your dataset contains a `store_id` field, you would specify `store_id` as a dimension to group sales forecasts for each store\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 10 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*`   
Required: No

 ** [ForecastFrequency](#API_CreateAutoPredictor_RequestSyntax) **   <a name="forecast-CreateAutoPredictor-request-ForecastFrequency"></a>
The frequency of predictions in a forecast\.  
Valid intervals are Y \(Year\), M \(Month\), W \(Week\), D \(Day\), H \(Hour\), 30min \(30 minutes\), 15min \(15 minutes\), 10min \(10 minutes\), 5min \(5 minutes\), and 1min \(1 minute\)\. For example, "Y" indicates every year and "5min" indicates every five minutes\.  
The frequency must be greater than or equal to the TARGET\_TIME\_SERIES dataset frequency\.  
When a RELATED\_TIME\_SERIES dataset is provided, the frequency must be equal to the RELATED\_TIME\_SERIES dataset frequency\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 5\.  
Pattern: `^Y|M|W|D|H|30min|15min|10min|5min|1min$`   
Required: No

 ** [ForecastHorizon](#API_CreateAutoPredictor_RequestSyntax) **   <a name="forecast-CreateAutoPredictor-request-ForecastHorizon"></a>
The number of time\-steps that the model predicts\. The forecast horizon is also called the prediction length\.  
The maximum forecast horizon is the lesser of 500 time\-steps or 1/4 of the TARGET\_TIME\_SERIES dataset length\. If you are retraining an existing AutoPredictor, then the maximum forecast horizon is the lesser of 500 time\-steps or 1/3 of the TARGET\_TIME\_SERIES dataset length\.  
If you are upgrading to an AutoPredictor or retraining an existing AutoPredictor, you cannot update the forecast horizon parameter\. You can meet this requirement by providing longer time\-series in the dataset\.  
Type: Integer  
Required: No

 ** [ForecastTypes](#API_CreateAutoPredictor_RequestSyntax) **   <a name="forecast-CreateAutoPredictor-request-ForecastTypes"></a>
The forecast types used to train a predictor\. You can specify up to five forecast types\. Forecast types can be quantiles from 0\.01 to 0\.99, by increments of 0\.01 or higher\. You can also specify the mean forecast with `mean`\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 20 items\.  
Length Constraints: Minimum length of 2\. Maximum length of 4\.  
Pattern: `(^0?\.\d\d?$|^mean$)`   
Required: No

 ** [OptimizationMetric](#API_CreateAutoPredictor_RequestSyntax) **   <a name="forecast-CreateAutoPredictor-request-OptimizationMetric"></a>
The accuracy metric used to optimize the predictor\.  
Type: String  
Valid Values:` WAPE | RMSE | AverageWeightedQuantileLoss | MASE | MAPE`   
Required: No

 ** [PredictorName](#API_CreateAutoPredictor_RequestSyntax) **   <a name="forecast-CreateAutoPredictor-request-PredictorName"></a>
A unique name for the predictor  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*`   
Required: Yes

 ** [ReferencePredictorArn](#API_CreateAutoPredictor_RequestSyntax) **   <a name="forecast-CreateAutoPredictor-request-ReferencePredictorArn"></a>
The ARN of the predictor to retrain or upgrade\. This parameter is only used when retraining or upgrading a predictor\. When creating a new predictor, do not specify a value for this parameter\.  
When upgrading or retraining a predictor, only specify values for the `ReferencePredictorArn` and `PredictorName`\. The value for `PredictorName` must be a unique predictor name\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: No

 ** [Tags](#API_CreateAutoPredictor_RequestSyntax) **   <a name="forecast-CreateAutoPredictor-request-Tags"></a>
Optional metadata to help you categorize and organize your predictors\. Each tag consists of a key and an optional value, both of which you define\. Tag keys and values are case sensitive\.  
The following restrictions apply to tags:  
+ For each resource, each tag key must be unique and each tag key must have one value\.
+ Maximum number of tags per resource: 50\.
+ Maximum key length: 128 Unicode characters in UTF\-8\.
+ Maximum value length: 256 Unicode characters in UTF\-8\.
+ Accepted characters: all letters and numbers, spaces representable in UTF\-8, and \+ \- = \. \_ : / @\. If your tagging schema is used across other services and resources, the character restrictions of those services also apply\. 
+ Key prefixes cannot include any upper or lowercase combination of `aws:` or `AWS:`\. Values can have this prefix\. If a tag value has `aws` as its prefix but the key does not, Forecast considers it to be a user tag and will count against the limit of 50 tags\. Tags with only the key prefix of `aws` do not count against your tags per resource limit\. You cannot edit or delete tag keys with this prefix\.
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Required: No

## Response Syntax<a name="API_CreateAutoPredictor_ResponseSyntax"></a>

```
{
   "PredictorArn": "string"
}
```

## Response Elements<a name="API_CreateAutoPredictor_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [PredictorArn](#API_CreateAutoPredictor_ResponseSyntax) **   <a name="forecast-CreateAutoPredictor-response-PredictorArn"></a>
The Amazon Resource Name \(ARN\) of the predictor\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

## Errors<a name="API_CreateAutoPredictor_Errors"></a>

 ** InvalidInputException **   
We can't process the request because it includes an invalid value or a value that exceeds the valid range\.  
HTTP Status Code: 400

 ** LimitExceededException **   
The limit on the number of resources per account has been exceeded\.  
HTTP Status Code: 400

 ** ResourceAlreadyExistsException **   
There is already a resource with this name\. Try again with a different name\.  
HTTP Status Code: 400

 ** ResourceInUseException **   
The specified resource is in use\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
We can't find a resource with that Amazon Resource Name \(ARN\)\. Check the ARN and try again\.  
HTTP Status Code: 400

## See Also<a name="API_CreateAutoPredictor_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/CreateAutoPredictor) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/CreateAutoPredictor) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/CreateAutoPredictor) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/CreateAutoPredictor) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/CreateAutoPredictor) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/CreateAutoPredictor) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/CreateAutoPredictor) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/CreateAutoPredictor) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/CreateAutoPredictor) 