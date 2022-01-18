# CreateExplainabilityExport<a name="API_CreateExplainabilityExport"></a>

Exports an Explainability resource created by the [CreateExplainability](API_CreateExplainability.md) operation\. Exported files are exported to an Amazon Simple Storage Service \(Amazon S3\) bucket\.

You must specify a [DataDestination](API_DataDestination.md) object that includes an Amazon S3 bucket and an AWS Identity and Access Management \(IAM\) role that Amazon Forecast can assume to access the Amazon S3 bucket\. For more information, see [Set Up Permissions for Amazon Forecast](aws-forecast-iam-roles.md)\.

**Note**  
The `Status` of the export job must be `ACTIVE` before you can access the export in your Amazon S3 bucket\. To get the status, use the [DescribeExplainabilityExport](API_DescribeExplainabilityExport.md) operation\.

## Request Syntax<a name="API_CreateExplainabilityExport_RequestSyntax"></a>

```
{
   "Destination": { 
      "S3Config": { 
         "KMSKeyArn": "string",
         "Path": "string",
         "RoleArn": "string"
      }
   },
   "ExplainabilityArn": "string",
   "ExplainabilityExportName": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateExplainabilityExport_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [Destination](#API_CreateExplainabilityExport_RequestSyntax) **   <a name="forecast-CreateExplainabilityExport-request-Destination"></a>
The destination for an export job\. Provide an S3 path, an AWS Identity and Access Management \(IAM\) role that allows Amazon Forecast to access the location, and an AWS Key Management Service \(KMS\) key \(optional\)\.   
Type: [DataDestination](API_DataDestination.md) object  
Required: Yes

 ** [ExplainabilityArn](#API_CreateExplainabilityExport_RequestSyntax) **   <a name="forecast-CreateExplainabilityExport-request-ExplainabilityArn"></a>
The Amazon Resource Name \(ARN\) of the Explainability to export\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: Yes

 ** [ExplainabilityExportName](#API_CreateExplainabilityExport_RequestSyntax) **   <a name="forecast-CreateExplainabilityExport-request-ExplainabilityExportName"></a>
A unique name for the Explainability export\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*`   
Required: Yes

 ** [Tags](#API_CreateExplainabilityExport_RequestSyntax) **   <a name="forecast-CreateExplainabilityExport-request-Tags"></a>
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

## Response Syntax<a name="API_CreateExplainabilityExport_ResponseSyntax"></a>

```
{
   "ExplainabilityExportArn": "string"
}
```

## Response Elements<a name="API_CreateExplainabilityExport_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ExplainabilityExportArn](#API_CreateExplainabilityExport_ResponseSyntax) **   <a name="forecast-CreateExplainabilityExport-response-ExplainabilityExportArn"></a>
The Amazon Resource Name \(ARN\) of the export\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

## Errors<a name="API_CreateExplainabilityExport_Errors"></a>

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

## See Also<a name="API_CreateExplainabilityExport_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/CreateExplainabilityExport) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/CreateExplainabilityExport) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/CreateExplainabilityExport) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/CreateExplainabilityExport) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/CreateExplainabilityExport) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/CreateExplainabilityExport) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/CreateExplainabilityExport) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/CreateExplainabilityExport) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/CreateExplainabilityExport) 