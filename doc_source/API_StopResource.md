# StopResource<a name="API_StopResource"></a>

Stops a resource\.

The resource undergoes the following states: `CREATE_STOPPING` and `CREATE_STOPPED`\. You cannot resume a resource once it has been stopped\.

This operation can be applied to the following resources \(and their corresponding child resources\):
+ Dataset Import Job
+ Predictor Job
+ Forecast Job
+ Forecast Export Job
+ Predictor Backtest Export Job

## Request Syntax<a name="API_StopResource_RequestSyntax"></a>

```
{
   "ResourceArn": "string"
}
```

## Request Parameters<a name="API_StopResource_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [ResourceArn](#API_StopResource_RequestSyntax) **   <a name="forecast-StopResource-request-ResourceArn"></a>
The Amazon Resource Name \(ARN\) that identifies the resource to stop\. The supported ARNs are `DatasetImportJobArn`, `PredictorArn`, `PredictorBacktestExportJobArn`, `ForecastArn`, and `ForecastExportJobArn`\.   
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: Yes

## Response Elements<a name="API_StopResource_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_StopResource_Errors"></a>

 **InvalidInputException**   
We can't process the request because it includes an invalid value or a value that exceeds the valid range\.  
HTTP Status Code: 400

 **LimitExceededException**   
The limit on the number of resources per account has been exceeded\.  
HTTP Status Code: 400

 **ResourceNotFoundException**   
We can't find a resource with that Amazon Resource Name \(ARN\)\. Check the ARN and try again\.  
HTTP Status Code: 400

## See Also<a name="API_StopResource_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/StopResource) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/StopResource) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/StopResource) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/StopResource) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/StopResource) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/StopResource) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/StopResource) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/StopResource) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/StopResource) 