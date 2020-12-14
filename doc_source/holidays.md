# Holidays Featurization<a name="holidays"></a>

 Holidays is a built\-in featurization that incorporates a feature\-engineered dataset of national holiday information into your model\. It provides native support for the holiday calendars of 66 countries\. To view the holiday calendars, refer to the [Jollyday library](http://jollyday.sourceforge.net/data.html)\. 

 The Holidays featurization is especially useful in the retail domain, where public holidays can significantly affect demand\. 

**Topics**
+ [Enabling the Holidays Featurization](#enabling-holidays)
+ [Country Codes](#holidays-country-codes)
+ [Additional Holiday Calendars](#holiday-calendars)

## Enabling the Holidays Featurization<a name="enabling-holidays"></a>

The Holidays featurization is included in Amazon Forecast as a [Supplementary Feature](API_SupplementaryFeature.md), and is enabled before training a predictor\. After you choose a country, Holidays applies that country’s holiday calendar to every item in your dataset during training\.

 You can enable Holidays using the Amazon Forecast console or the Forecast Software Development Kit \(SDK\)\.

------
#### [ Forecast SDK ]

Using the [ `CreatePredictor`](API_CreatePredictor.md) operation, enable Holidays by adding `"Name": "holiday`" and setting `"Value"` to a two\-letter country code\. See [Country Codes](#holidays-country-codes)\.

For example, to include the USA holiday calendar, use the following code\.

```
      "InputDataConfig": {          
        "SupplementaryFeatures": [          
            {             
                "Name": "holiday",            
                "Value": "US"         
            }      
            ]   
        },
```

------
#### [ Forecast Console ]

Choose a country from the **Country for Holidays** drop\-down during the **Train Predictor** stage\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/holidays-dropdown.png)

------

## Country Codes<a name="holidays-country-codes"></a>

 Amazon Forecast provides native support for the public holiday calendars of the following countries\. Use the **Country Code** when specifying a country with the API\.


**Supported Countries**  

| Country | Country Code | 
| --- | --- | 
|   Albania   |   "AL"   | 
|   Argentina   |   "AR"   | 
|   Austria   |   "AT"   | 
|   Australia   |   "AU"   | 
|  Bosnia Herzegovina |   "BA"   | 
|   Belgium   |   "BE"   | 
|   Bulgaria   |   "BG"   | 
|   Bolivia   |   "BO"   | 
|   Brazil   |   "BR"   | 
|   Belarus   |   "BY"   | 
|   Canada   |   "CA"   | 
|   Chile   |   "CL"   | 
|   Colombia   |   "CO"   | 
|   Costa Rica  |   "CR"   | 
|   Croatia   |   "HR"   | 
|   Czech Republic   |   "CZ"   | 
|   Denmark   |   "DK"   | 
|   Ecuador   |   "EC"   | 
|   Estonia   |   "EE"   | 
|   Ethiopia   |   "ET"   | 
|   Finland   |   "FI"   | 
|   France   |   "FR"   | 
|   Germany   |   "DE"   | 
|   Greece   |   "GR"   | 
|   Hungary   |   "HU"   | 
|   Iceland   |   "IS"   | 
|   India   |   "IN"   | 
|   Ireland   |   "IE"   | 
|   Italy   |   "IT"   | 
|   Japan   |   "JP"   | 
|   Kazakhstan   |   "KZ"   | 
|   Korea   |   "KR"   | 
|   Latvia   |   "LV"   | 
|   Liechtenstein   |   "LI"   | 
|   Lithuania   |   "LT"   | 
|   Luxembourg   |   "LU"   | 
|   Macedonia   |   "MK"   | 
|   Malta   |   "MT"   | 
|   Mexico   |   "MX"   | 
|   Moldova   |   "MD"   | 
|   Montenegro   |   "ME"   | 
|   Netherlands   |   "NL"   | 
|   New Zealand  |   "NZ"   | 
|   Nicaragua   |   "NI"   | 
|   Nigeria   |   "NG"   | 
|   Norway   |   "NO"   | 
|   Panama   |   "PA"   | 
|   Paraguay   |   "PY"   | 
|   Peru   |   "PE"   | 
|   Poland   |   "PL"   | 
|   Portugal   |   "PT"   | 
|   Romania   |   "RO"   | 
|   Russia   |   "RU"   | 
|   Serbia   |   "RS"   | 
|   Slovakia   |   "SK"   | 
|   Slovenia   |   "SI"   | 
|   South Africa  |   "ZA"   | 
|   Spain   |   "ES"   | 
|   Sweden   |   "SE"   | 
|   Switzerland   |   "CH"   | 
|   Ukraine   |   "UA"   | 
|   United Arab Emirates  |   "AE"   | 
|   United States  |   "US"   | 
|   United Kingdom   |   "UK"   | 
|   Uruguay   |   "UY"   | 
|   Venezuela   |   "VE"   | 

## Additional Holiday Calendars<a name="holiday-calendars"></a>

Amazon Forecast includes the holiday calendars from the [Jollyday library](http://jollyday.sourceforge.net/data.html) and also supports holidays for India, Korea, and United Arab Emirates\. Their holidays are listed below\.

------
#### [ India \- "IN" ]

January 26 \- Republic Day 

August 15 \- Independence Day

October 2 \- Gandhi Jayanti

------
#### [ Korea \- "KR" ]

January 1 \- New Year 

March 1 \- Independence Movement Day 

May 5 \- Children's Day

June 6 \- Memorial Day

August 15 \- Liberation Day

October 3 \- National Foundation Day

October 9 \- Hangul Day

December 25 \- Christmas Day

------
#### [ United Arab Emirates \- "AE" ]

January 1 \- New Year 

December 1 \- Commemoration Day

December 2\-3 \- National Day

Ramadan\*

Eid al\-Fitr\*

Eid al\-Adha\*

Islamic New Year\*

\*islamic Holidays Are Determined by Lunar Cycles\.

------