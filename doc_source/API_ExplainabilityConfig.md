# ExplainabilityConfig<a name="API_ExplainabilityConfig"></a>

The ExplainabilityConfig data type defines the number of time series and time points included in [CreateExplainability](API_CreateExplainability.md)\.

If you provide a predictor ARN for `ResourceArn`, you must set both `TimePointGranularity` and `TimeSeriesGranularity` to “ALL”\. When creating Predictor Explainability, Amazon Forecast considers all time series and time points\.

If you provide a forecast ARN for `ResourceArn`, you can set `TimePointGranularity` and `TimeSeriesGranularity` to either “ALL” or “Specific”\.

## Contents<a name="API_ExplainabilityConfig_Contents"></a>

 ** TimePointGranularity **   <a name="forecast-Type-ExplainabilityConfig-TimePointGranularity"></a>
To create an Explainability for all time points in your forecast horizon, use `ALL`\. To create an Explainability for specific time points in your forecast horizon, use `SPECIFIC`\.  
Specify time points with the `StartDateTime` and `EndDateTime` parameters within the [CreateExplainability](API_CreateExplainability.md) operation\.  
Type: String  
Valid Values:` ALL | SPECIFIC`   
Required: Yes

 ** TimeSeriesGranularity **   <a name="forecast-Type-ExplainabilityConfig-TimeSeriesGranularity"></a>
To create an Explainability for all time series in your datasets, use `ALL`\. To create an Explainability for specific time series in your datasets, use `SPECIFIC`\.  
Specify time series by uploading a CSV file to an Amazon S3 bucket and set the location within the [DataDestination](API_DataDestination.md) data type\.  
Type: String  
Valid Values:` ALL | SPECIFIC`   
Required: Yes

## See Also<a name="API_ExplainabilityConfig_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/ExplainabilityConfig) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/ExplainabilityConfig) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/ExplainabilityConfig) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/ExplainabilityConfig) 