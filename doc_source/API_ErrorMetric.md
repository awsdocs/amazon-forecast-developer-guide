# ErrorMetric<a name="API_ErrorMetric"></a>

 Provides detailed error metrics to evaluate the performance of a predictor\. This object is part of the [Metrics](API_Metrics.md) object\. 

## Contents<a name="API_ErrorMetric_Contents"></a>

 ** ForecastType **   <a name="forecast-Type-ErrorMetric-ForecastType"></a>
 The Forecast type used to compute WAPE, MAPE, MASE, and RMSE\.   
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 4\.  
Pattern: `(^0?\.\d\d?$|^mean$)`   
Required: No

 ** MAPE **   <a name="forecast-Type-ErrorMetric-MAPE"></a>
The Mean Absolute Percentage Error \(MAPE\)  
Type: Double  
Required: No

 ** MASE **   <a name="forecast-Type-ErrorMetric-MASE"></a>
The Mean Absolute Scaled Error \(MASE\)  
Type: Double  
Required: No

 ** RMSE **   <a name="forecast-Type-ErrorMetric-RMSE"></a>
 The root\-mean\-square error \(RMSE\)\.   
Type: Double  
Required: No

 ** WAPE **   <a name="forecast-Type-ErrorMetric-WAPE"></a>
 The weighted absolute percentage error \(WAPE\)\.   
Type: Double  
Required: No

## See Also<a name="API_ErrorMetric_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/ErrorMetric) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/ErrorMetric) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/ErrorMetric) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/ErrorMetric) 