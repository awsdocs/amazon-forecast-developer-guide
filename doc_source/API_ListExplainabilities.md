# ListExplainabilities<a name="API_ListExplainabilities"></a>

Returns a list of Explainability resources created using the [CreateExplainability](API_CreateExplainability.md) operation\. This operation returns a summary for each Explainability\. You can filter the list using an array of [Filter](API_Filter.md) objects\.

To retrieve the complete set of properties for a particular Explainability resource, use the ARN with the [DescribeExplainability](API_DescribeExplainability.md) operation\.

## Request Syntax<a name="API_ListExplainabilities_RequestSyntax"></a>

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

## Request Parameters<a name="API_ListExplainabilities_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [Filters](#API_ListExplainabilities_RequestSyntax) **   <a name="forecast-ListExplainabilities-request-Filters"></a>
An array of filters\. For each filter, provide a condition and a match statement\. The condition is either `IS` or `IS_NOT`, which specifies whether to include or exclude the resources that match the statement from the list\. The match statement consists of a key and a value\.  
 **Filter properties**   
+  `Condition` \- The condition to apply\. Valid values are `IS` and `IS_NOT`\.
+  `Key` \- The name of the parameter to filter on\. Valid values are `ResourceArn` and `Status`\.
+  `Value` \- The value to match\.
Type: Array of [Filter](API_Filter.md) objects  
Required: No

 ** [MaxResults](#API_ListExplainabilities_RequestSyntax) **   <a name="forecast-ListExplainabilities-request-MaxResults"></a>
The number of items returned in the response\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListExplainabilities_RequestSyntax) **   <a name="forecast-ListExplainabilities-request-NextToken"></a>
If the result of the previous request was truncated, the response includes a NextToken\. To retrieve the next set of results, use the token in the next request\. Tokens expire after 24 hours\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 3000\.  
Pattern: `.+`   
Required: No

## Response Syntax<a name="API_ListExplainabilities_ResponseSyntax"></a>

```
{
   "Explainabilities": [ 
      { 
         "CreationTime": number,
         "ExplainabilityArn": "string",
         "ExplainabilityConfig": { 
            "TimePointGranularity": "string",
            "TimeSeriesGranularity": "string"
         },
         "ExplainabilityName": "string",
         "LastModificationTime": number,
         "Message": "string",
         "ResourceArn": "string",
         "Status": "string"
      }
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListExplainabilities_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Explainabilities](#API_ListExplainabilities_ResponseSyntax) **   <a name="forecast-ListExplainabilities-response-Explainabilities"></a>
An array of objects that summarize the properties of each Explainability resource\.  
Type: Array of [ExplainabilitySummary](API_ExplainabilitySummary.md) objects

 ** [NextToken](#API_ListExplainabilities_ResponseSyntax) **   <a name="forecast-ListExplainabilities-response-NextToken"></a>
Returns this token if the response is truncated\. To retrieve the next set of results, use the token in the next request\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 3000\.  
Pattern: `.+` 

## Errors<a name="API_ListExplainabilities_Errors"></a>

 ** InvalidInputException **   
We can't process the request because it includes an invalid value or a value that exceeds the valid range\.  
HTTP Status Code: 400

 ** InvalidNextTokenException **   
The token is not valid\. Tokens expire after 24 hours\.  
HTTP Status Code: 400

## See Also<a name="API_ListExplainabilities_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/ListExplainabilities) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/ListExplainabilities) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/ListExplainabilities) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/ListExplainabilities) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/ListExplainabilities) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/ListExplainabilities) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/ListExplainabilities) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/ListExplainabilities) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/ListExplainabilities) 