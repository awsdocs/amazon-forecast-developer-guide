# DescribeExplainabilityExport<a name="API_DescribeExplainabilityExport"></a>

Describes an Explainability export created using the [CreateExplainabilityExport](API_CreateExplainabilityExport.md) operation\.

## Request Syntax<a name="API_DescribeExplainabilityExport_RequestSyntax"></a>

```
{
   "ExplainabilityExportArn": "string"
}
```

## Request Parameters<a name="API_DescribeExplainabilityExport_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [ExplainabilityExportArn](#API_DescribeExplainabilityExport_RequestSyntax) **   <a name="forecast-DescribeExplainabilityExport-request-ExplainabilityExportArn"></a>
The Amazon Resource Name \(ARN\) of the Explainability export\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: Yes

## Response Syntax<a name="API_DescribeExplainabilityExport_ResponseSyntax"></a>

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
   "ExplainabilityArn": "string",
   "ExplainabilityExportArn": "string",
   "ExplainabilityExportName": "string",
   "LastModificationTime": number,
   "Message": "string",
   "Status": "string"
}
```

## Response Elements<a name="API_DescribeExplainabilityExport_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CreationTime](#API_DescribeExplainabilityExport_ResponseSyntax) **   <a name="forecast-DescribeExplainabilityExport-response-CreationTime"></a>
When the Explainability export was created\.  
Type: Timestamp

 ** [Destination](#API_DescribeExplainabilityExport_ResponseSyntax) **   <a name="forecast-DescribeExplainabilityExport-response-Destination"></a>
The destination for an export job\. Provide an S3 path, an AWS Identity and Access Management \(IAM\) role that allows Amazon Forecast to access the location, and an AWS Key Management Service \(KMS\) key \(optional\)\.   
Type: [DataDestination](API_DataDestination.md) object

 ** [ExplainabilityArn](#API_DescribeExplainabilityExport_ResponseSyntax) **   <a name="forecast-DescribeExplainabilityExport-response-ExplainabilityArn"></a>
The Amazon Resource Name \(ARN\) of the Explainability\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

 ** [ExplainabilityExportArn](#API_DescribeExplainabilityExport_ResponseSyntax) **   <a name="forecast-DescribeExplainabilityExport-response-ExplainabilityExportArn"></a>
The Amazon Resource Name \(ARN\) of the Explainability export\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

 ** [ExplainabilityExportName](#API_DescribeExplainabilityExport_ResponseSyntax) **   <a name="forecast-DescribeExplainabilityExport-response-ExplainabilityExportName"></a>
The name of the Explainability export\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*` 

 ** [LastModificationTime](#API_DescribeExplainabilityExport_ResponseSyntax) **   <a name="forecast-DescribeExplainabilityExport-response-LastModificationTime"></a>
The last time the resource was modified\. The timestamp depends on the status of the job:  
+  `CREATE_PENDING` \- The `CreationTime`\.
+  `CREATE_IN_PROGRESS` \- The current timestamp\.
+  `CREATE_STOPPING` \- The current timestamp\.
+  `CREATE_STOPPED` \- When the job stopped\.
+  `ACTIVE` or `CREATE_FAILED` \- When the job finished or failed\.
Type: Timestamp

 ** [Message](#API_DescribeExplainabilityExport_ResponseSyntax) **   <a name="forecast-DescribeExplainabilityExport-response-Message"></a>
Information about any errors that occurred during the export\.  
Type: String

 ** [Status](#API_DescribeExplainabilityExport_ResponseSyntax) **   <a name="forecast-DescribeExplainabilityExport-response-Status"></a>
The status of the Explainability export\. States include:   
+  `ACTIVE` 
+  `CREATE_PENDING`, `CREATE_IN_PROGRESS`, `CREATE_FAILED` 
+  `CREATE_STOPPING`, `CREATE_STOPPED` 
+  `DELETE_PENDING`, `DELETE_IN_PROGRESS`, `DELETE_FAILED` 
Type: String  
Length Constraints: Maximum length of 256\.

## Errors<a name="API_DescribeExplainabilityExport_Errors"></a>

 ** InvalidInputException **   
We can't process the request because it includes an invalid value or a value that exceeds the valid range\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
We can't find a resource with that Amazon Resource Name \(ARN\)\. Check the ARN and try again\.  
HTTP Status Code: 400

## See Also<a name="API_DescribeExplainabilityExport_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/DescribeExplainabilityExport) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/DescribeExplainabilityExport) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/DescribeExplainabilityExport) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/DescribeExplainabilityExport) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/DescribeExplainabilityExport) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/DescribeExplainabilityExport) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/DescribeExplainabilityExport) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/DescribeExplainabilityExport) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/DescribeExplainabilityExport) 