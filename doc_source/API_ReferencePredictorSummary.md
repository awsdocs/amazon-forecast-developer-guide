# ReferencePredictorSummary<a name="API_ReferencePredictorSummary"></a>

Provides a summary of the reference predictor used when retraining or upgrading a predictor\.

## Contents<a name="API_ReferencePredictorSummary_Contents"></a>

 ** Arn **   <a name="forecast-Type-ReferencePredictorSummary-Arn"></a>
The ARN of the reference predictor\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: No

 ** State **   <a name="forecast-Type-ReferencePredictorSummary-State"></a>
Whether the reference predictor is `Active` or `Deleted`\.  
Type: String  
Valid Values:` Active | Deleted`   
Required: No

## See Also<a name="API_ReferencePredictorSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/ReferencePredictorSummary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/ReferencePredictorSummary) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/ReferencePredictorSummary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/ReferencePredictorSummary) 