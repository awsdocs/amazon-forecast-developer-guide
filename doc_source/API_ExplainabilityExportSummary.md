# ExplainabilityExportSummary<a name="API_ExplainabilityExportSummary"></a>

Provides a summary of the Explainability export properties used in the [ListExplainabilityExports](API_ListExplainabilityExports.md) operation\. To get a complete set of properties, call the [DescribeExplainabilityExport](API_DescribeExplainabilityExport.md) operation, and provide the `ExplainabilityExportArn`\.

## Contents<a name="API_ExplainabilityExportSummary_Contents"></a>

 ** CreationTime **   <a name="forecast-Type-ExplainabilityExportSummary-CreationTime"></a>
When the Explainability was created\.  
Type: Timestamp  
Required: No

 ** Destination **   <a name="forecast-Type-ExplainabilityExportSummary-Destination"></a>
The destination for an export job\. Provide an S3 path, an AWS Identity and Access Management \(IAM\) role that allows Amazon Forecast to access the location, and an AWS Key Management Service \(KMS\) key \(optional\)\.   
Type: [DataDestination](API_DataDestination.md) object  
Required: No

 ** ExplainabilityExportArn **   <a name="forecast-Type-ExplainabilityExportSummary-ExplainabilityExportArn"></a>
The Amazon Resource Name \(ARN\) of the Explainability export\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: No

 ** ExplainabilityExportName **   <a name="forecast-Type-ExplainabilityExportSummary-ExplainabilityExportName"></a>
The name of the Explainability export  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*`   
Required: No

 ** LastModificationTime **   <a name="forecast-Type-ExplainabilityExportSummary-LastModificationTime"></a>
The last time the resource was modified\. The timestamp depends on the status of the job:  
+  `CREATE_PENDING` \- The `CreationTime`\.
+  `CREATE_IN_PROGRESS` \- The current timestamp\.
+  `CREATE_STOPPING` \- The current timestamp\.
+  `CREATE_STOPPED` \- When the job stopped\.
+  `ACTIVE` or `CREATE_FAILED` \- When the job finished or failed\.
Type: Timestamp  
Required: No

 ** Message **   <a name="forecast-Type-ExplainabilityExportSummary-Message"></a>
Information about any errors that may have occurred during the Explainability export\.  
Type: String  
Required: No

 ** Status **   <a name="forecast-Type-ExplainabilityExportSummary-Status"></a>
The status of the Explainability export\. States include:   
+  `ACTIVE` 
+  `CREATE_PENDING`, `CREATE_IN_PROGRESS`, `CREATE_FAILED` 
+  `CREATE_STOPPING`, `CREATE_STOPPED` 
+  `DELETE_PENDING`, `DELETE_IN_PROGRESS`, `DELETE_FAILED` 
Type: String  
Length Constraints: Maximum length of 256\.  
Required: No

## See Also<a name="API_ExplainabilityExportSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/ExplainabilityExportSummary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/ExplainabilityExportSummary) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/ExplainabilityExportSummary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/ExplainabilityExportSummary) 