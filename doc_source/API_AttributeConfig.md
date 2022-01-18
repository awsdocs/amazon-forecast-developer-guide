# AttributeConfig<a name="API_AttributeConfig"></a>

Provides information about the method used to transform attributes\.

The following is an example using the RETAIL domain:

 `{` 

 `"AttributeName": "demand",` 

 `"Transformations": {"aggregation": "sum", "middlefill": "zero", "backfill": "zero"}` 

 `}` 

## Contents<a name="API_AttributeConfig_Contents"></a>

 ** AttributeName **   <a name="forecast-Type-AttributeConfig-AttributeName"></a>
The name of the attribute as specified in the schema\. Amazon Forecast supports the target field of the target time series and the related time series datasets\. For example, for the RETAIL domain, the target is `demand`\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*`   
Required: Yes

 ** Transformations **   <a name="forecast-Type-AttributeConfig-Transformations"></a>
The method parameters \(key\-value pairs\), which are a map of override parameters\. Specify these parameters to override the default values\. Related Time Series attributes do not accept aggregation parameters\.  
The following list shows the parameters and their valid values for the "filling" featurization method for a **Target Time Series** dataset\. Default values are bolded\.  
+  `aggregation`: **sum**, `avg`, `first`, `min`, `max` 
+  `frontfill`: **none** 
+  `middlefill`: **zero**, `nan` \(not a number\), `value`, `median`, `mean`, `min`, `max` 
+  `backfill`: **zero**, `nan`, `value`, `median`, `mean`, `min`, `max` 
The following list shows the parameters and their valid values for a **Related Time Series** featurization method \(there are no defaults\):  
+  `middlefill`: `zero`, `value`, `median`, `mean`, `min`, `max` 
+  `backfill`: `zero`, `value`, `median`, `mean`, `min`, `max` 
+  `futurefill`: `zero`, `value`, `median`, `mean`, `min`, `max` 
To set a filling method to a specific value, set the fill parameter to `value` and define the value in a corresponding `_value` parameter\. For example, to set backfilling to a value of 2, include the following: `"backfill": "value"` and `"backfill_value":"2"`\.   
Type: String to string map  
Map Entries: Maximum number of 20 items\.  
Key Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Key Pattern: `^[a-zA-Z][a-zA-Z0-9_]*`   
Value Length Constraints: Maximum length of 256\.  
Value Pattern: `^[a-zA-Z0-9\_\-]+$`   
Required: Yes

## See Also<a name="API_AttributeConfig_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/AttributeConfig) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/AttributeConfig) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/AttributeConfig) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/AttributeConfig) 