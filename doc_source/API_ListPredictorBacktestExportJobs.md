# ListPredictorBacktestExportJobs<a name="API_ListPredictorBacktestExportJobs"></a>

Returns a list of predictor backtest export jobs created using the [CreatePredictorBacktestExportJob](API_CreatePredictorBacktestExportJob.md) operation\. This operation returns a summary for each backtest export job\. You can filter the list using an array of [Filter](API_Filter.md) objects\.

To retrieve the complete set of properties for a particular backtest export job, use the ARN with the [DescribePredictorBacktestExportJob](API_DescribePredictorBacktestExportJob.md) operation\.

## Request Syntax<a name="API_ListPredictorBacktestExportJobs_RequestSyntax"></a>

```
{
   "Filters": [ 
      { 
         "Condition": "string",
         "Key": "string",
         "Value": "string"
      }
   ],
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListPredictorBacktestExportJobs_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [Filters](#API_ListPredictorBacktestExportJobs_RequestSyntax) **   <a name="forecast-ListPredictorBacktestExportJobs-request-Filters"></a>
An array of filters\. For each filter, provide a condition and a match statement\. The condition is either `IS` or `IS_NOT`, which specifies whether to include or exclude the predictor backtest export jobs that match the statement from the list\. The match statement consists of a key and a value\.  
 **Filter properties**   
+  `Condition` \- The condition to apply\. Valid values are `IS` and `IS_NOT`\. To include the predictor backtest export jobs that match the statement, specify `IS`\. To exclude matching predictor backtest export jobs, specify `IS_NOT`\.
+  `Key` \- The name of the parameter to filter on\. Valid values are `PredictorArn` and `Status`\.
+  `Value` \- The value to match\.
Type: Array of [Filter](API_Filter.md) objects  
Required: No

 ** [MaxResults](#API_ListPredictorBacktestExportJobs_RequestSyntax) **   <a name="forecast-ListPredictorBacktestExportJobs-request-MaxResults"></a>
The number of items to return in the response\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListPredictorBacktestExportJobs_RequestSyntax) **   <a name="forecast-ListPredictorBacktestExportJobs-request-NextToken"></a>
If the result of the previous request was truncated, the response includes a NextToken\. To retrieve the next set of results, use the token in the next request\. Tokens expire after 24 hours\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 3000\.  
Pattern: `.+`   
Required: No

## Response Syntax<a name="API_ListPredictorBacktestExportJobs_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "PredictorBacktestExportJobs": [ 
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
         "PredictorBacktestExportJobArn": "string",
         "PredictorBacktestExportJobName": "string",
         "Status": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListPredictorBacktestExportJobs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_ListPredictorBacktestExportJobs_ResponseSyntax) **   <a name="forecast-ListPredictorBacktestExportJobs-response-NextToken"></a>
Returns this token if the response is truncated\. To retrieve the next set of results, use the token in the next request\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 3000\.  
Pattern: `.+` 

 ** [PredictorBacktestExportJobs](#API_ListPredictorBacktestExportJobs_ResponseSyntax) **   <a name="forecast-ListPredictorBacktestExportJobs-response-PredictorBacktestExportJobs"></a>
An array of objects that summarize the properties of each predictor backtest export job\.  
Type: Array of [PredictorBacktestExportJobSummary](API_PredictorBacktestExportJobSummary.md) objects

## Errors<a name="API_ListPredictorBacktestExportJobs_Errors"></a>

 ** InvalidInputException **   
We can't process the request because it includes an invalid value or a value that exceeds the valid range\.  
HTTP Status Code: 400

 ** InvalidNextTokenException **   
The token is not valid\. Tokens expire after 24 hours\.  
HTTP Status Code: 400

## See Also<a name="API_ListPredictorBacktestExportJobs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/ListPredictorBacktestExportJobs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/ListPredictorBacktestExportJobs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/ListPredictorBacktestExportJobs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/ListPredictorBacktestExportJobs) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/ListPredictorBacktestExportJobs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/ListPredictorBacktestExportJobs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/ListPredictorBacktestExportJobs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/ListPredictorBacktestExportJobs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/ListPredictorBacktestExportJobs) 