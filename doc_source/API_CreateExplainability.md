# CreateExplainability<a name="API_CreateExplainability"></a>

**Note**  
Explainability is only available for Forecasts and Predictors generated from an AutoPredictor \([CreateAutoPredictor](API_CreateAutoPredictor.md)\)

Creates an Amazon Forecast Explainability\.

Explainability helps you better understand how the attributes in your datasets impact forecast\. Amazon Forecast uses a metric called Impact scores to quantify the relative impact of each attribute and determine whether they increase or decrease forecast values\.

To enable Forecast Explainability, your predictor must include at least one of the following: related time series, item metadata, or additional datasets like Holidays and the Weather Index\.

CreateExplainability accepts either a Predictor ARN or Forecast ARN\. To receive aggregated Impact scores for all time series and time points in your datasets, provide a Predictor ARN\. To receive Impact scores for specific time series and time points, provide a Forecast ARN\.

 **CreateExplainability with a Predictor ARN** 

**Note**  
You can only have one Explainability resource per predictor\. If you already enabled `ExplainPredictor` in [CreateAutoPredictor](API_CreateAutoPredictor.md), that predictor already has an Explainability resource\.

The following parameters are required when providing a Predictor ARN:
+  `ExplainabilityName` \- A unique name for the Explainability\.
+  `ResourceArn` \- The Arn of the predictor\.
+  `TimePointGranularity` \- Must be set to “ALL”\.
+  `TimeSeriesGranularity` \- Must be set to “ALL”\.

Do not specify a value for the following parameters:
+  `DataSource` \- Only valid when TimeSeriesGranularity is “SPECIFIC”\.
+  `Schema` \- Only valid when TimeSeriesGranularity is “SPECIFIC”\.
+  `StartDateTime` \- Only valid when TimePointGranularity is “SPECIFIC”\.
+  `EndDateTime` \- Only valid when TimePointGranularity is “SPECIFIC”\.

 **CreateExplainability with a Forecast ARN** 

**Note**  
You can specify a maximum of 50 time series and 500 time points\.

The following parameters are required when providing a Predictor ARN:
+  `ExplainabilityName` \- A unique name for the Explainability\.
+  `ResourceArn` \- The Arn of the forecast\.
+  `TimePointGranularity` \- Either “ALL” or “SPECIFIC”\.
+  `TimeSeriesGranularity` \- Either “ALL” or “SPECIFIC”\.

If you set TimeSeriesGranularity to “SPECIFIC”, you must also provide the following:
+  `DataSource` \- The S3 location of the CSV file specifying your time series\.
+  `Schema` \- The Schema defines the attributes and attribute types listed in the Data Source\.

If you set TimePointGranularity to “SPECIFIC”, you must also provide the following:
+  `StartDateTime` \- The first timestamp in the range of time points\.
+  `EndDateTime` \- The last timestamp in the range of time points\.

## Request Syntax<a name="API_CreateExplainability_RequestSyntax"></a>

```
{
   "DataSource": { 
      "S3Config": { 
         "KMSKeyArn": "string",
         "Path": "string",
         "RoleArn": "string"
      }
   },
   "EnableVisualization": boolean,
   "EndDateTime": "string",
   "ExplainabilityConfig": { 
      "TimePointGranularity": "string",
      "TimeSeriesGranularity": "string"
   },
   "ExplainabilityName": "string",
   "ResourceArn": "string",
   "Schema": { 
      "Attributes": [ 
         { 
            "AttributeName": "string",
            "AttributeType": "string"
         }
      ]
   },
   "StartDateTime": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateExplainability_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [DataSource](#API_CreateExplainability_RequestSyntax) **   <a name="forecast-CreateExplainability-request-DataSource"></a>
The source of your data, an AWS Identity and Access Management \(IAM\) role that allows Amazon Forecast to access the data and, optionally, an AWS Key Management Service \(KMS\) key\.  
Type: [DataSource](API_DataSource.md) object  
Required: No

 ** [EnableVisualization](#API_CreateExplainability_RequestSyntax) **   <a name="forecast-CreateExplainability-request-EnableVisualization"></a>
Create an Expainability visualization that is viewable within the AWS console\.  
Type: Boolean  
Required: No

 ** [EndDateTime](#API_CreateExplainability_RequestSyntax) **   <a name="forecast-CreateExplainability-request-EndDateTime"></a>
If `TimePointGranularity` is set to `SPECIFIC`, define the last time point for the Explainability\.  
Use the following timestamp format: yyyy\-MM\-ddTHH:mm:ss \(example: 2015\-01\-01T20:00:00\)  
Type: String  
Length Constraints: Maximum length of 19\.  
Pattern: `^\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}$`   
Required: No

 ** [ExplainabilityConfig](#API_CreateExplainability_RequestSyntax) **   <a name="forecast-CreateExplainability-request-ExplainabilityConfig"></a>
The configuration settings that define the granularity of time series and time points for the Explainability\.  
Type: [ExplainabilityConfig](API_ExplainabilityConfig.md) object  
Required: Yes

 ** [ExplainabilityName](#API_CreateExplainability_RequestSyntax) **   <a name="forecast-CreateExplainability-request-ExplainabilityName"></a>
A unique name for the Explainability\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*`   
Required: Yes

 ** [ResourceArn](#API_CreateExplainability_RequestSyntax) **   <a name="forecast-CreateExplainability-request-ResourceArn"></a>
The Amazon Resource Name \(ARN\) of the Predictor or Forecast used to create the Explainability\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: Yes

 ** [Schema](#API_CreateExplainability_RequestSyntax) **   <a name="forecast-CreateExplainability-request-Schema"></a>
Defines the fields of a dataset\.  
Type: [Schema](API_Schema.md) object  
Required: No

 ** [StartDateTime](#API_CreateExplainability_RequestSyntax) **   <a name="forecast-CreateExplainability-request-StartDateTime"></a>
If `TimePointGranularity` is set to `SPECIFIC`, define the first point for the Explainability\.  
Use the following timestamp format: yyyy\-MM\-ddTHH:mm:ss \(example: 2015\-01\-01T20:00:00\)  
Type: String  
Length Constraints: Maximum length of 19\.  
Pattern: `^\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}$`   
Required: No

 ** [Tags](#API_CreateExplainability_RequestSyntax) **   <a name="forecast-CreateExplainability-request-Tags"></a>
Optional metadata to help you categorize and organize your resources\. Each tag consists of a key and an optional value, both of which you define\. Tag keys and values are case sensitive\.  
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

## Response Syntax<a name="API_CreateExplainability_ResponseSyntax"></a>

```
{
   "ExplainabilityArn": "string"
}
```

## Response Elements<a name="API_CreateExplainability_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ExplainabilityArn](#API_CreateExplainability_ResponseSyntax) **   <a name="forecast-CreateExplainability-response-ExplainabilityArn"></a>
The Amazon Resource Name \(ARN\) of the Explainability\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

## Errors<a name="API_CreateExplainability_Errors"></a>

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

## See Also<a name="API_CreateExplainability_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/CreateExplainability) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/CreateExplainability) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/CreateExplainability) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/CreateExplainability) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/CreateExplainability) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/CreateExplainability) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/CreateExplainability) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/CreateExplainability) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/CreateExplainability) 