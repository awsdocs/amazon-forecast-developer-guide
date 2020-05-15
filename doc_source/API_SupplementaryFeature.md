# SupplementaryFeature<a name="API_SupplementaryFeature"></a>

Describes a supplementary feature of a dataset group\. This object is part of the [InputDataConfig](API_InputDataConfig.md) object\.

The only supported feature is a holiday calendar\. If you use the calendar, all data in the datasets should belong to the same country as the calendar\. For the holiday calendar data, see the [Jollyday](http://jollyday.sourceforge.net/data.html) web site\.

India and Korea's holidays are not included in the Jollyday library, but both are supported by Amazon Forecast\. Their holidays are:

 **"IN" \- INDIA** 
+  `JANUARY 26 - REPUBLIC DAY` 
+  `AUGUST 15 - INDEPENDENCE DAY` 
+  `OCTOBER 2 GANDHI'S BIRTHDAY` 

 **"KR" \- KOREA** 
+  `JANUARY 1 - NEW YEAR` 
+  `MARCH 1 - INDEPENDENCE MOVEMENT DAY` 
+  `MAY 5 - CHILDREN'S DAY` 
+  `JUNE 6 - MEMORIAL DAY` 
+  `AUGUST 15 - LIBERATION DAY` 
+  `OCTOBER 3 - NATIONAL FOUNDATION DAY` 
+  `OCTOBER 9 - HANGEUL DAY` 
+  `DECEMBER 25 - CHRISTMAS DAY` 

## Contents<a name="API_SupplementaryFeature_Contents"></a>

 **Name**   <a name="forecast-Type-SupplementaryFeature-Name"></a>
The name of the feature\. This must be "holiday"\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*`   
Required: Yes

 **Value**   <a name="forecast-Type-SupplementaryFeature-Value"></a>
One of the following 2 letter country codes:  
+ "AR" \- ARGENTINA
+ "AT" \- AUSTRIA
+ "AU" \- AUSTRALIA
+ "BE" \- BELGIUM
+ "BR" \- BRAZIL
+ "CA" \- CANADA
+ "CN" \- CHINA
+ "CZ" \- CZECH REPUBLIC
+ "DK" \- DENMARK
+ "EC" \- ECUADOR
+ "FI" \- FINLAND
+ "FR" \- FRANCE
+ "DE" \- GERMANY
+ "HU" \- HUNGARY
+ "IE" \- IRELAND
+ "IN" \- INDIA
+ "IT" \- ITALY
+ "JP" \- JAPAN
+ "KR" \- KOREA
+ "LU" \- LUXEMBOURG
+ "MX" \- MEXICO
+ "NL" \- NETHERLANDS
+ "NO" \- NORWAY
+ "PL" \- POLAND
+ "PT" \- PORTUGAL
+ "RU" \- RUSSIA
+ "ZA" \- SOUTH AFRICA
+ "ES" \- SPAIN
+ "SE" \- SWEDEN
+ "CH" \- SWITZERLAND
+ "US" \- UNITED STATES
+ "UK" \- UNITED KINGDOM
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\_\-]+$`   
Required: Yes

## See Also<a name="API_SupplementaryFeature_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/SupplementaryFeature) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/SupplementaryFeature) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/forecast-2018-06-26/SupplementaryFeature) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/SupplementaryFeature) 