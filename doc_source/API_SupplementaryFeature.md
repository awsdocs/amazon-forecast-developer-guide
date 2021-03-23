# SupplementaryFeature<a name="API_SupplementaryFeature"></a>

Describes a supplementary feature of a dataset group\. This object is part of the [InputDataConfig](API_InputDataConfig.md) object\. Forecast supports the Weather Index and Holidays built\-in featurizations\.

 **Weather Index** 

The Amazon Forecast Weather Index is a built\-in featurization that incorporates historical and projected weather information into your model\. The Weather Index supplements your datasets with over two years of historical weather data and up to 14 days of projected weather data\. For more information, see [Amazon Forecast Weather Index](https://docs.aws.amazon.com/forecast/latest/dg/weather.html)\.

 **Holidays** 

Holidays is a built\-in featurization that incorporates a feature\-engineered dataset of national holiday information into your model\. It provides native support for the holiday calendars of 66 countries\. To view the holiday calendars, refer to the [Jollyday](http://jollyday.sourceforge.net/data.html) library\. For more information, see [Holidays Featurization](https://docs.aws.amazon.com/forecast/latest/dg/holidays.html)\.

## Contents<a name="API_SupplementaryFeature_Contents"></a>

 **Name**   <a name="forecast-Type-SupplementaryFeature-Name"></a>
The name of the feature\. Valid values: `"holiday"` and `"weather"`\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*`   
Required: Yes

 **Value**   <a name="forecast-Type-SupplementaryFeature-Value"></a>
 **Weather Index**   
To enable the Weather Index, set the value to `"true"`   
 **Holidays**   
To enable Holidays, specify a country with one of the following two\-letter country codes:  
+ "AL" \- ALBANIA
+ "AR" \- ARGENTINA
+ "AT" \- AUSTRIA
+ "AU" \- AUSTRALIA
+ "BA" \- BOSNIA HERZEGOVINA
+ "BE" \- BELGIUM
+ "BG" \- BULGARIA
+ "BO" \- BOLIVIA
+ "BR" \- BRAZIL
+ "BY" \- BELARUS
+ "CA" \- CANADA
+ "CL" \- CHILE
+ "CO" \- COLOMBIA
+ "CR" \- COSTA RICA
+ "HR" \- CROATIA
+ "CZ" \- CZECH REPUBLIC
+ "DK" \- DENMARK
+ "EC" \- ECUADOR
+ "EE" \- ESTONIA
+ "ET" \- ETHIOPIA
+ "FI" \- FINLAND
+ "FR" \- FRANCE
+ "DE" \- GERMANY
+ "GR" \- GREECE
+ "HU" \- HUNGARY
+ "IS" \- ICELAND
+ "IN" \- INDIA
+ "IE" \- IRELAND
+ "IT" \- ITALY
+ "JP" \- JAPAN
+ "KZ" \- KAZAKHSTAN
+ "KR" \- KOREA
+ "LV" \- LATVIA
+ "LI" \- LIECHTENSTEIN
+ "LT" \- LITHUANIA
+ "LU" \- LUXEMBOURG
+ "MK" \- MACEDONIA
+ "MT" \- MALTA
+ "MX" \- MEXICO
+ "MD" \- MOLDOVA
+ "ME" \- MONTENEGRO
+ "NL" \- NETHERLANDS
+ "NZ" \- NEW ZEALAND
+ "NI" \- NICARAGUA
+ "NG" \- NIGERIA
+ "NO" \- NORWAY
+ "PA" \- PANAMA
+ "PY" \- PARAGUAY
+ "PE" \- PERU
+ "PL" \- POLAND
+ "PT" \- PORTUGAL
+ "RO" \- ROMANIA
+ "RU" \- RUSSIA
+ "RS" \- SERBIA
+ "SK" \- SLOVAKIA
+ "SI" \- SLOVENIA
+ "ZA" \- SOUTH AFRICA
+ "ES" \- SPAIN
+ "SE" \- SWEDEN
+ "CH" \- SWITZERLAND
+ "UA" \- UKRAINE
+ "AE" \- UNITED ARAB EMIRATES
+ "US" \- UNITED STATES
+ "UK" \- UNITED KINGDOM
+ "UY" \- URUGUAY
+ "VE" \- VENEZUELA
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\_\-]+$`   
Required: Yes

## See Also<a name="API_SupplementaryFeature_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/SupplementaryFeature) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/SupplementaryFeature) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/SupplementaryFeature) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/SupplementaryFeature) 