# ExplainabilityInfo<a name="API_ExplainabilityInfo"></a>

Provides information about the Explainability resource\.

## Contents<a name="API_ExplainabilityInfo_Contents"></a>

 ** ExplainabilityArn **   <a name="forecast-Type-ExplainabilityInfo-ExplainabilityArn"></a>
The Amazon Resource Name \(ARN\) of the Explainability\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: No

 ** Status **   <a name="forecast-Type-ExplainabilityInfo-Status"></a>
The status of the Explainability\. States include:   
+  `ACTIVE` 
+  `CREATE_PENDING`, `CREATE_IN_PROGRESS`, `CREATE_FAILED` 
+  `CREATE_STOPPING`, `CREATE_STOPPED` 
+  `DELETE_PENDING`, `DELETE_IN_PROGRESS`, `DELETE_FAILED` 
Type: String  
Length Constraints: Maximum length of 256\.  
Required: No

## See Also<a name="API_ExplainabilityInfo_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/ExplainabilityInfo) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/ExplainabilityInfo) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/ExplainabilityInfo) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/ExplainabilityInfo) 