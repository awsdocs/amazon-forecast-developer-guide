# DescribePredictorBacktestExportJob<a name="API_DescribePredictorBacktestExportJob"></a>

Describes a predictor backtest export job created using the [CreatePredictorBacktestExportJob](API_CreatePredictorBacktestExportJob.md) operation\.

In addition to listing the properties provided by the user in the `CreatePredictorBacktestExportJob` request, this operation lists the following properties:
+  `CreationTime` 
+  `LastModificationTime` 
+  `Status` 
+  `Message` \(if an error occurred\)

## Request Syntax<a name="API_DescribePredictorBacktestExportJob_RequestSyntax"></a>

```
{
   "PredictorBacktestExportJobArn": "string"
}
```

## Request Parameters<a name="API_DescribePredictorBacktestExportJob_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [PredictorBacktestExportJobArn](#API_DescribePredictorBacktestExportJob_RequestSyntax) **   <a name="forecast-DescribePredictorBacktestExportJob-request-PredictorBacktestExportJobArn"></a>
The Amazon Resource Name \(ARN\) of the predictor backtest export job\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: Yes

## Response Syntax<a name="API_DescribePredictorBacktestExportJob_ResponseSyntax"></a>

```
{
   "CreationTime": number,
   "Destination": { 
      "S3Config": { 
         "KMSKeyArn": "string",
         "Path": "string",
         "RoleArn": "string"
      }
   },
   "LastModificationTime": number,
   "Message": "string",
   "PredictorArn": "string",
   "PredictorBacktestExportJobArn": "string",
   "PredictorBacktestExportJobName": "string",
   "Status": "string"
}
```

## Response Elements<a name="API_DescribePredictorBacktestExportJob_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CreationTime](#API_DescribePredictorBacktestExportJob_ResponseSyntax) **   <a name="forecast-DescribePredictorBacktestExportJob-response-CreationTime"></a>
When the predictor backtest export job was created\.  
Type: Timestamp

 ** [Destination](#API_DescribePredictorBacktestExportJob_ResponseSyntax) **   <a name="forecast-DescribePredictorBacktestExportJob-response-Destination"></a>
The destination for an export job\. Provide an S3 path, an AWS Identity and Access Management \(IAM\) role that allows Amazon Forecast to access the location, and an AWS Key Management Service \(KMS\) key \(optional\)\.   
Type: [DataDestination](API_DataDestination.md) object

 ** [LastModificationTime](#API_DescribePredictorBacktestExportJob_ResponseSyntax) **   <a name="forecast-DescribePredictorBacktestExportJob-response-LastModificationTime"></a>
When the last successful export job finished\.  
Type: Timestamp

 ** [Message](#API_DescribePredictorBacktestExportJob_ResponseSyntax) **   <a name="forecast-DescribePredictorBacktestExportJob-response-Message"></a>
Information about any errors that may have occurred during the backtest export\.  
Type: String

 ** [PredictorArn](#API_DescribePredictorBacktestExportJob_ResponseSyntax) **   <a name="forecast-DescribePredictorBacktestExportJob-response-PredictorArn"></a>
The Amazon Resource Name \(ARN\) of the predictor\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

 ** [PredictorBacktestExportJobArn](#API_DescribePredictorBacktestExportJob_ResponseSyntax) **   <a name="forecast-DescribePredictorBacktestExportJob-response-PredictorBacktestExportJobArn"></a>
The Amazon Resource Name \(ARN\) of the predictor backtest export job\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

 ** [PredictorBacktestExportJobName](#API_DescribePredictorBacktestExportJob_ResponseSyntax) **   <a name="forecast-DescribePredictorBacktestExportJob-response-PredictorBacktestExportJobName"></a>
The name of the predictor backtest export job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*` 

 ** [Status](#API_DescribePredictorBacktestExportJob_ResponseSyntax) **   <a name="forecast-DescribePredictorBacktestExportJob-response-Status"></a>
The status of the predictor backtest export job\. States include:   
+  `ACTIVE` 
+  `CREATE_PENDING` 
+  `CREATE_IN_PROGRESS` 
+  `CREATE_FAILED` 
+  `DELETE_PENDING` 
+  `DELETE_IN_PROGRESS` 
+  `DELETE_FAILED` 
Type: String  
Length Constraints: Maximum length of 256\.

## Errors<a name="API_DescribePredictorBacktestExportJob_Errors"></a>

 **InvalidInputException**   
We can't process the request because it includes an invalid value or a value that exceeds the valid range\.  
HTTP Status Code: 400

 **ResourceNotFoundException**   
We can't find a resource with that Amazon Resource Name \(ARN\)\. Check the ARN and try again\.  
HTTP Status Code: 400

## See Also<a name="API_DescribePredictorBacktestExportJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/DescribePredictorBacktestExportJob) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/DescribePredictorBacktestExportJob) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/DescribePredictorBacktestExportJob) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/DescribePredictorBacktestExportJob) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/forecast-2018-06-26/DescribePredictorBacktestExportJob) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/DescribePredictorBacktestExportJob) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/DescribePredictorBacktestExportJob) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/DescribePredictorBacktestExportJob) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/DescribePredictorBacktestExportJob) 