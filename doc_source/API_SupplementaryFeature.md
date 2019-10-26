# SupplementaryFeature<a name="API_SupplementaryFeature"></a>

Describes a supplementary feature of a dataset group\. This object is part of the [InputDataConfig](API_InputDataConfig.md) object\.

The only supported feature is a holiday calendar\. If you use the calendar, all data in the datasets should belong to the same country as the calendar\. For the holiday calendar data, see the [Jollyday](http://jollyday.sourceforge.net/data.html) web site\.

## Contents<a name="API_SupplementaryFeature_Contents"></a>

 **Name**   <a name="forecast-Type-SupplementaryFeature-Name"></a>
The name of the feature\. This must be "holiday"\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*`   
Required: Yes

 **Value**   <a name="forecast-Type-SupplementaryFeature-Value"></a>
One of the following 2 letter country codes:  
+ "AU" \- AUSTRALIA
+ "DE" \- GERMANY
+ "JP" \- JAPAN
+ "US" \- UNITED\_STATES
+ "UK" \- UNITED\_KINGDOM
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\_\-]+$`   
Required: Yes

## See Also<a name="API_SupplementaryFeature_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/SupplementaryFeature) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/SupplementaryFeature) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/forecast-2018-06-26/SupplementaryFeature) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/forecast-2018-06-26/SupplementaryFeature) 