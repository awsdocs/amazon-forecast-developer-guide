# ExplainabilitySummary<a name="API_ExplainabilitySummary"></a>

Provides a summary of the Explainability properties used in the [ListExplainabilities](API_ListExplainabilities.md) operation\. To get a complete set of properties, call the [DescribeExplainability](API_DescribeExplainability.md) operation, and provide the listed `ExplainabilityArn`\.

## Contents<a name="API_ExplainabilitySummary_Contents"></a>

 ** CreationTime **   <a name="forecast-Type-ExplainabilitySummary-CreationTime"></a>
When the Explainability was created\.  
Type: Timestamp  
Required: No

 ** ExplainabilityArn **   <a name="forecast-Type-ExplainabilitySummary-ExplainabilityArn"></a>
The Amazon Resource Name \(ARN\) of the Explainability\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: No

 ** ExplainabilityConfig **   <a name="forecast-Type-ExplainabilitySummary-ExplainabilityConfig"></a>
The configuration settings that define the granularity of time series and time points for the Explainability\.  
Type: [ExplainabilityConfig](API_ExplainabilityConfig.md) object  
Required: No

 ** ExplainabilityName **   <a name="forecast-Type-ExplainabilitySummary-ExplainabilityName"></a>
The name of the Explainability\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*`   
Required: No

 ** LastModificationTime **   <a name="forecast-Type-ExplainabilitySummary-LastModificationTime"></a>
The last time the resource was modified\. The timestamp depends on the status of the job:  
+  `CREATE_PENDING` \- The `CreationTime`\.
+  `CREATE_IN_PROGRESS` \- The current timestamp\.
+  `CREATE_STOPPING` \- The current timestamp\.
+  `CREATE_STOPPED` \- When the job stopped\.
+  `ACTIVE` or `CREATE_FAILED` \- When the job finished or failed\.
Type: Timestamp  
Required: No

 ** Message **   <a name="forecast-Type-ExplainabilitySummary-Message"></a>
Information about any errors that may have occurred during the Explainability creation process\.  
Type: String  
Required: No

 ** ResourceArn **   <a name="forecast-Type-ExplainabilitySummary-ResourceArn"></a>
The Amazon Resource Name \(ARN\) of the Predictor or Forecast used to create the Explainability\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: No

 ** Status **   <a name="forecast-Type-ExplainabilitySummary-Status"></a>
The status of the Explainability\. States include:   
+  `ACTIVE` 
+  `CREATE_PENDING`, `CREATE_IN_PROGRESS`, `CREATE_FAILED` 
+  `CREATE_STOPPING`, `CREATE_STOPPED` 
+  `DELETE_PENDING`, `DELETE_IN_PROGRESS`, `DELETE_FAILED` 
Type: String  
Length Constraints: Maximum length of 256\.  
Required: No

## See Also<a name="API_ExplainabilitySummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/ExplainabilitySummary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/ExplainabilitySummary) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/ExplainabilitySummary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/ExplainabilitySummary) 