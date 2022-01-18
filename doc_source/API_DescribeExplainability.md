# DescribeExplainability<a name="API_DescribeExplainability"></a>

Describes an Explainability resource created using the [CreateExplainability](API_CreateExplainability.md) operation\.

## Request Syntax<a name="API_DescribeExplainability_RequestSyntax"></a>

```
{
   "ExplainabilityArn": "string"
}
```

## Request Parameters<a name="API_DescribeExplainability_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [ExplainabilityArn](#API_DescribeExplainability_RequestSyntax) **   <a name="forecast-DescribeExplainability-request-ExplainabilityArn"></a>
The Amazon Resource Name \(ARN\) of the Explaianability to describe\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: Yes

## Response Syntax<a name="API_DescribeExplainability_ResponseSyntax"></a>

```
{
   "CreationTime": number,
   "DataSource": { 
      "S3Config": { 
         "KMSKeyArn": "string",
         "Path": "string",
         "RoleArn": "string"
      }
   },
   "EnableVisualization": boolean,
   "EndDateTime": "string",
   "EstimatedTimeRemainingInMinutes": number,
   "ExplainabilityArn": "string",
   "ExplainabilityConfig": { 
      "TimePointGranularity": "string",
      "TimeSeriesGranularity": "string"
   },
   "ExplainabilityName": "string",
   "LastModificationTime": number,
   "Message": "string",
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
   "Status": "string"
}
```

## Response Elements<a name="API_DescribeExplainability_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CreationTime](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-CreationTime"></a>
When the Explainability resource was created\.  
Type: Timestamp

 ** [DataSource](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-DataSource"></a>
The source of your data, an AWS Identity and Access Management \(IAM\) role that allows Amazon Forecast to access the data and, optionally, an AWS Key Management Service \(KMS\) key\.  
Type: [DataSource](API_DataSource.md) object

 ** [EnableVisualization](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-EnableVisualization"></a>
Whether the visualization was enabled for the Explainability resource\.  
Type: Boolean

 ** [EndDateTime](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-EndDateTime"></a>
If `TimePointGranularity` is set to `SPECIFIC`, the last time point in the Explainability\.  
Type: String  
Length Constraints: Maximum length of 19\.  
Pattern: `^\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}$` 

 ** [EstimatedTimeRemainingInMinutes](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-EstimatedTimeRemainingInMinutes"></a>
The estimated time remaining in minutes for the [CreateExplainability](API_CreateExplainability.md) job to complete\.  
Type: Long

 ** [ExplainabilityArn](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-ExplainabilityArn"></a>
The Amazon Resource Name \(ARN\) of the Explainability\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

 ** [ExplainabilityConfig](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-ExplainabilityConfig"></a>
The configuration settings that define the granularity of time series and time points for the Explainability\.  
Type: [ExplainabilityConfig](API_ExplainabilityConfig.md) object

 ** [ExplainabilityName](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-ExplainabilityName"></a>
The name of the Explainability\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*` 

 ** [LastModificationTime](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-LastModificationTime"></a>
The last time the resource was modified\. The timestamp depends on the status of the job:  
+  `CREATE_PENDING` \- The `CreationTime`\.
+  `CREATE_IN_PROGRESS` \- The current timestamp\.
+  `CREATE_STOPPING` \- The current timestamp\.
+  `CREATE_STOPPED` \- When the job stopped\.
+  `ACTIVE` or `CREATE_FAILED` \- When the job finished or failed\.
Type: Timestamp

 ** [Message](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-Message"></a>
If an error occurred, a message about the error\.  
Type: String

 ** [ResourceArn](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-ResourceArn"></a>
The Amazon Resource Name \(ARN\) of the Predictor or Forecast used to create the Explainability resource\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

 ** [Schema](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-Schema"></a>
Defines the fields of a dataset\.  
Type: [Schema](API_Schema.md) object

 ** [StartDateTime](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-StartDateTime"></a>
If `TimePointGranularity` is set to `SPECIFIC`, the first time point in the Explainability\.  
Type: String  
Length Constraints: Maximum length of 19\.  
Pattern: `^\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}$` 

 ** [Status](#API_DescribeExplainability_ResponseSyntax) **   <a name="forecast-DescribeExplainability-response-Status"></a>
The status of the Explainability resource\. States include:   
+  `ACTIVE` 
+  `CREATE_PENDING`, `CREATE_IN_PROGRESS`, `CREATE_FAILED` 
+  `CREATE_STOPPING`, `CREATE_STOPPED` 
+  `DELETE_PENDING`, `DELETE_IN_PROGRESS`, `DELETE_FAILED` 
Type: String  
Length Constraints: Maximum length of 256\.

## Errors<a name="API_DescribeExplainability_Errors"></a>

 ** InvalidInputException **   
We can't process the request because it includes an invalid value or a value that exceeds the valid range\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
We can't find a resource with that Amazon Resource Name \(ARN\)\. Check the ARN and try again\.  
HTTP Status Code: 400

## See Also<a name="API_DescribeExplainability_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/DescribeExplainability) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/DescribeExplainability) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/DescribeExplainability) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/DescribeExplainability) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/DescribeExplainability) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/DescribeExplainability) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/DescribeExplainability) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/DescribeExplainability) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/DescribeExplainability) 