# DeleteResourceTree<a name="API_DeleteResourceTree"></a>

Deletes an entire resource tree\. This operation will delete the parent resource and its child resources\.

Child resources are resources that were created from another resource\. For example, when a forecast is generated from a predictor, the forecast is the child resource and the predictor is the parent resource\.

Amazon Forecast resources possess the following parent\-child resource hierarchies:
+  **Dataset**: dataset import jobs
+  **Dataset Group**: predictors, predictor backtest export jobs, forecasts, forecast export jobs
+  **Predictor**: predictor backtest export jobs, forecasts, forecast export jobs
+  **Forecast**: forecast export jobs

**Note**  
 `DeleteResourceTree` will only delete Amazon Forecast resources, and will not delete datasets or exported files stored in Amazon S3\. 

## Request Syntax<a name="API_DeleteResourceTree_RequestSyntax"></a>

```
{
   "ResourceArn": "string"
}
```

## Request Parameters<a name="API_DeleteResourceTree_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [ResourceArn](#API_DeleteResourceTree_RequestSyntax) **   <a name="forecast-DeleteResourceTree-request-ResourceArn"></a>
The Amazon Resource Name \(ARN\) of the parent resource to delete\. All child resources of the parent resource will also be deleted\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: Yes

## Response Elements<a name="API_DeleteResourceTree_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_DeleteResourceTree_Errors"></a>

 ** InvalidInputException **   
We can't process the request because it includes an invalid value or a value that exceeds the valid range\.  
HTTP Status Code: 400

 ** ResourceInUseException **   
The specified resource is in use\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
We can't find a resource with that Amazon Resource Name \(ARN\)\. Check the ARN and try again\.  
HTTP Status Code: 400

## See Also<a name="API_DeleteResourceTree_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/DeleteResourceTree) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/DeleteResourceTree) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/DeleteResourceTree) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/DeleteResourceTree) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/DeleteResourceTree) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/DeleteResourceTree) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/DeleteResourceTree) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/DeleteResourceTree) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/DeleteResourceTree) 