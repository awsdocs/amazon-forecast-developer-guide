# FeaturizationMethod<a name="API_FeaturizationMethod"></a>

Provides information about the method that featurizes \(transforms\) a dataset field\. The method is part of the `FeaturizationPipeline` of the [Featurization](API_Featurization.md) object\. If you don't specify `FeaturizationMethodParameters`, Amazon Forecast uses default parameters\.

The following is an example of how you specify a `FeaturizationMethod` object\.

 `{` 

 `"FeaturizationMethodName": "filling",` 

 `"FeaturizationMethodParameters": {"aggregation": "avg", "backfill": "nan"}` 

 `}` 

## Contents<a name="API_FeaturizationMethod_Contents"></a>

 **FeaturizationMethodName**   <a name="forecast-Type-FeaturizationMethod-FeaturizationMethodName"></a>
The name of the method\. The "filling" method is the only supported method\.  
Type: String  
Valid Values:` filling`   
Required: Yes

 **FeaturizationMethodParameters**   <a name="forecast-Type-FeaturizationMethod-FeaturizationMethodParameters"></a>
The method parameters \(key\-value pairs\)\. Specify these parameters to override the default values\. The following list shows the parameters and their valid values\. Bold signifies the default value\.  
+  `aggregation`: **sum**, `avg`, `first`, `min`, `max` 
+  `frontfill`: **none** 
+  `middlefill`: **zero**, `nan` \(not a number\)
+  `backfill`: **zero**, `nan` 
Type: String to string map  
Key Length Constraints: Maximum length of 256\.  
Key Pattern: `^[a-zA-Z0-9\-\_\.\/\[\]\,\\]+$`   
Value Length Constraints: Maximum length of 256\.  
Value Pattern: `^[a-zA-Z0-9\-\_\.\/\[\]\,\"\\\s]+$`   
Required: No

## See Also<a name="API_FeaturizationMethod_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/FeaturizationMethod) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/FeaturizationMethod) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/forecast-2018-06-26/FeaturizationMethod) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/forecast-2018-06-26/FeaturizationMethod) 