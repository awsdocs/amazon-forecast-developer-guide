# DeletePredictorBacktestExportJob<a name="API_DeletePredictorBacktestExportJob"></a>

Deletes a predictor backtest export job\.

## Request Syntax<a name="API_DeletePredictorBacktestExportJob_RequestSyntax"></a>

```
{
   "PredictorBacktestExportJobArn": "string"
}
```

## Request Parameters<a name="API_DeletePredictorBacktestExportJob_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [PredictorBacktestExportJobArn](#API_DeletePredictorBacktestExportJob_RequestSyntax) **   <a name="forecast-DeletePredictorBacktestExportJob-request-PredictorBacktestExportJobArn"></a>
The Amazon Resource Name \(ARN\) of the predictor backtest export job to delete\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: Yes

## Response Elements<a name="API_DeletePredictorBacktestExportJob_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_DeletePredictorBacktestExportJob_Errors"></a>

 **InvalidInputException**   
We can't process the request because it includes an invalid value or a value that exceeds the valid range\.  
HTTP Status Code: 400

 **ResourceInUseException**   
The specified resource is in use\.  
HTTP Status Code: 400

 **ResourceNotFoundException**   
We can't find a resource with that Amazon Resource Name \(ARN\)\. Check the ARN and try again\.  
HTTP Status Code: 400

## See Also<a name="API_DeletePredictorBacktestExportJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/DeletePredictorBacktestExportJob) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/DeletePredictorBacktestExportJob) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/DeletePredictorBacktestExportJob) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/DeletePredictorBacktestExportJob) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/DeletePredictorBacktestExportJob) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/DeletePredictorBacktestExportJob) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/DeletePredictorBacktestExportJob) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/DeletePredictorBacktestExportJob) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/DeletePredictorBacktestExportJob) 