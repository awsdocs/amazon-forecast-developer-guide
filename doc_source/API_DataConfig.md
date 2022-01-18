# DataConfig<a name="API_DataConfig"></a>

The data configuration for your dataset group and any additional datasets\.

## Contents<a name="API_DataConfig_Contents"></a>

 ** AdditionalDatasets **   <a name="forecast-Type-DataConfig-AdditionalDatasets"></a>
Additional built\-in datasets like Holidays and the Weather Index\.  
Type: Array of [AdditionalDataset](API_AdditionalDataset.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 2 items\.  
Required: No

 ** AttributeConfigs **   <a name="forecast-Type-DataConfig-AttributeConfigs"></a>
Aggregation and filling options for attributes in your dataset group\.  
Type: Array of [AttributeConfig](API_AttributeConfig.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** DatasetGroupArn **   <a name="forecast-Type-DataConfig-DatasetGroupArn"></a>
The ARN of the dataset group used to train the predictor\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: Yes

## See Also<a name="API_DataConfig_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/DataConfig) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/DataConfig) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/DataConfig) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/DataConfig) 