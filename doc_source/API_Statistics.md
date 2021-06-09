# Statistics<a name="API_Statistics"></a>

Provides statistics for each data field imported into to an Amazon Forecast dataset with the [CreateDatasetImportJob](API_CreateDatasetImportJob.md) operation\.

## Contents<a name="API_Statistics_Contents"></a>

 **Avg**   <a name="forecast-Type-Statistics-Avg"></a>
For a numeric field, the average value in the field\.  
Type: Double  
Required: No

 **Count**   <a name="forecast-Type-Statistics-Count"></a>
The number of values in the field\. If the response value is \-1, refer to `CountLong`\.  
Type: Integer  
Required: No

 **CountDistinct**   <a name="forecast-Type-Statistics-CountDistinct"></a>
The number of distinct values in the field\. If the response value is \-1, refer to `CountDistinctLong`\.  
Type: Integer  
Required: No

 **CountDistinctLong**   <a name="forecast-Type-Statistics-CountDistinctLong"></a>
The number of distinct values in the field\. `CountDistinctLong` is used instead of `CountDistinct` if the value is greater than 2,147,483,647\.  
Type: Long  
Required: No

 **CountLong**   <a name="forecast-Type-Statistics-CountLong"></a>
The number of values in the field\. `CountLong` is used instead of `Count` if the value is greater than 2,147,483,647\.  
Type: Long  
Required: No

 **CountNan**   <a name="forecast-Type-Statistics-CountNan"></a>
The number of NAN \(not a number\) values in the field\. If the response value is \-1, refer to `CountNanLong`\.  
Type: Integer  
Required: No

 **CountNanLong**   <a name="forecast-Type-Statistics-CountNanLong"></a>
The number of NAN \(not a number\) values in the field\. `CountNanLong` is used instead of `CountNan` if the value is greater than 2,147,483,647\.  
Type: Long  
Required: No

 **CountNull**   <a name="forecast-Type-Statistics-CountNull"></a>
The number of null values in the field\. If the response value is \-1, refer to `CountNullLong`\.  
Type: Integer  
Required: No

 **CountNullLong**   <a name="forecast-Type-Statistics-CountNullLong"></a>
The number of null values in the field\. `CountNullLong` is used instead of `CountNull` if the value is greater than 2,147,483,647\.  
Type: Long  
Required: No

 **Max**   <a name="forecast-Type-Statistics-Max"></a>
For a numeric field, the maximum value in the field\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\_]+$`   
Required: No

 **Min**   <a name="forecast-Type-Statistics-Min"></a>
For a numeric field, the minimum value in the field\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\_]+$`   
Required: No

 **Stddev**   <a name="forecast-Type-Statistics-Stddev"></a>
For a numeric field, the standard deviation\.  
Type: Double  
Required: No

## See Also<a name="API_Statistics_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/Statistics) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/Statistics) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/Statistics) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/Statistics) 