# Weather Index<a name="weather"></a>

The Amazon Forecast Weather Index is a built\-in featurization that incorporates historical and projected weather information into your model\. It is especially useful for retail use cases, where temperature and precipitation can significantly impact demand\.

When the Weather Index is enabled, Forecast only applies the weather featurization to time series where it finds improvements in accuracy during predictor training\. If supplementing a time series with weather information does not improve its predictive accuracy during backtesting, Forecast will not apply the Weather Index to that particular time series\.

In order to apply the Weather Index, you must include a [geolocation attribute](#adding-geolocation) in your target time series and any related time series datasets\. You also need to specify [time zones](#specifying-timezones) for your target time series timestamps\. For more information, refer to the [Conditions and Restrictions](#weather-conditions-restrictions) section\.

**Topics**
+ [Enabling the Weather Index](#enabling-weather)
+ [Adding Geolocation information](#adding-geolocation)
+ [Specifying time zones](#specifying-timezones)
+ [Conditions and Restrictions](#weather-conditions-restrictions)

## Enabling the Weather Index<a name="enabling-weather"></a>

The Weather Index is enabled during the predictor training stage\. It can be applied when running AutoML or manually selecting the CNN\-QR, DeepAR\+, or Prophet algorithms\. The Weather Index is included in the [SupplementaryFeature](API_SupplementaryFeature.md) data type when using the Forecast API\.

Before enabling the Weather Index, you must include a geolocation attribute in your target time series and related timeseries datsets, and define the time zones for your timestamps\. For more information, see [Adding Geolocation Information](#adding-geolocation) and [Specifying Time Zones](#specifying-timezones)\.

You can enable the Weather Index using the Amazon Forecast console and the Amazon Forecast Software Development Kit \(SDK\) \.

------
#### [ Forecast Console ]

**To enable the Weather Index**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From the **Dataset groups** list, choose your dataset group\.

1. On the left sidebar, choose **Predictors**\.

1. Choose **Train new predictor**\.

1. Choose **Enable Weather Index**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/enable-weather.PNG)

------
#### [ Forecast SDK ]

**To enable the Weather Index**

Using the [ `CreatePredictor`](API_CreatePredictor.md) operation, enable the Weather Index by adding `"Name": "weather"` and `"Value": "true"` in the [SupplementaryFeature](API_SupplementaryFeature.md) data type\.

```
    "InputDataConfig": { 
        ...
        "SupplementaryFeatures": [
            ...                      
            {             
                "Name": "weather",            
                "Value": "true"         
            }      
            ]   
        },
```

------

## Adding Geolocation information<a name="adding-geolocation"></a>

In order to use the Weather Index, your target time series and related time series datasets must include a geolocation attribute that specifies the location of each item\. This attribute can be formatted in one of two ways:
+ **Latitude & Longitude** \(US and Europe\) \- the latitude and longitude in decimal format \(Example: 47\.61\_\-122\.33\)\.
+ **Postal code** \(US Only\) \- the country code \(US\), followed by the 5\-digit ZIP code \(Example: US\_98121\)\.

All geolocation values must be exclusively within either the US \(excluding Hawaii and Alaska\) or Europe region\. Your dataset cannot contain items in *both* the US and Europe\. The Postal code format only applies to US locations\.

**Topics**
+ [Latitude & Longitude Bounds](#geolocation-bounds)
+ [Including geolocation in your dataset schema](#geolocation-schema)
+ [Setting the geolocation format](#geolocation-format)

### Latitude & Longitude Bounds<a name="geolocation-bounds"></a>

When using the Latitude & Longitude format, Forecast applies the following bounds for the US and Europe regions:

------
#### [ US Region ]

**Bounds**: latitude \(24\.6, 50\.0\), longitude \(\-126\.0, \-66\.4\)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/weather-us-bounds.png)

------
#### [ Europe Region ]

**Bounds**: latitude \(34\.8, 71\.8\), longitude \(\-12\.6, \-44\.8\)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/weather-euro-bounds.png)

------

### Including geolocation in your dataset schema<a name="geolocation-schema"></a>

Using the console or [CreateDataset](API_CreateDataset.md) operation, define the location attribute type as 'geolocation' within the JSON schema for the target time series and any related time series\. The attributes in the schema must be ordered as they appear in the datasets\.

```
 { 
  "Attributes":[
    {
       "AttributeName": "timestamp",
       "AttributeType": "timestamp"
    },
    {
       "AttributeName": "target_value",
       "AttributeType": "float"
    },
    {
       "AttributeName": "item_id",
       "AttributeType": "string"
    },
    {
       "AttributeName": "location",
       "AttributeType": "geolocation"
    }
  ]
}
```

### Setting the geolocation format<a name="geolocation-format"></a>

The format of the geolocation attribute can be in the **Postal Code** or **Latitude & Longitude** format\. You can set the geolocation format using the Forecast console and the Forecast Software Development Kit \(SDK\)\.

------
#### [ Forecast Console ]

**To add a geolocation attribute to a target time series dataset**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. Choose **Create dataset group**\.

1. In the **Schema builder**, set your geolocation **Attribute type** to `geolocation`\.

1. In the **Location format** drop\-down, choose your location format\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/schema-builder-geolocation.png)

You can also define your attributes in JSON format and select a location format from the **Location format** drop\-down\.

------
#### [ Forecast SDK ]

**To add a geolocation attribute to a time series dataset**

Using the [ CreateDatasetImportJob](API_CreateDatasetImportJob.md) operation, set the value of `GeolocationFormat` to one of the following: 
+ **Latitude & longitude** \(US and Europe\): `"LAT_LONG"`
+ **Postal code** \(US Only\): `"CC_POSTALCODE"`

For example, to specify the latitude & longitude format, include the following in `CreateDatasetImportJob` request:

```
{
    ...
    "GeolocationFormat": "LAT_LONG"
}
```

------

## Specifying time zones<a name="specifying-timezones"></a>

You can either let Amazon Forecast automatically synchronize your time zone information with your geolocation attribute, or you can manually assign a single time zone to your entire data set\. 

**Topics**
+ [Automatically sync time zones with geolocation](#timezones-automatic)
+ [Manually select time zone](#timezones-manual)

### Automatically sync time zones with geolocation<a name="timezones-automatic"></a>

This option is ideal for datasets that contain timestamps in multiple time zones and those timestamps are expressed in local time\. Forecast will assign a time zone for every item in the target time series dataset based on the item’s geolocation attribute\.

You can automatically sync your timestamps with your geolocation attribute using the Forecast console and Forecast SDK\.

------
#### [ Forecast Console ]

**To sync time zones with the geolocation attribute**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. Choose **Create dataset group**\.

1. In **Dataset import details**, choose **Sync time zone with location**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/sync-timezone-with-geolocation.PNG)

------
#### [ Forecast SDK ]

**To sync time zones with the geolocation attribute**

Using the [ CreateDatasetImportJob](API_CreateDatasetImportJob.md) operation, set `"UseGeolocationForTimeZone"` to `"true"`\.

```
{
    ...
    "UseGeolocationForTimeZone": "true"
}
```

------

### Manually select time zone<a name="timezones-manual"></a>

**Note**  
You can manually select a time zone outside of the *US region* and *Europe region*\. However, all geolocation values must still be within Europe or the US\.

This option is ideal for datasets with all timestamps within a single time zone, or if all timestamps are normalized to a single time zone\. Using this option will apply the same time zone to every item in the dataset\.

The Weather Index accepts the following time zones:

 **US region** 
+  America/Los\_Angeles 
+  America/Phoenix 
+  America/Denver 
+  America/Chicago 
+  America/New\_York 

 **Europe region** 
+  Europe/London 
+  Europe/Paris 
+  Europe/Helsinki 

 **Other** 
+  Etc/GMT\+12 
+  Pacific/Midway 
+  Pacific/Honolulu 
+  Pacific/Marquesas 
+  America/Anchorage 
+  America/Caracas 
+  America/Puerto\_Rico 
+  America/St\_Johns 
+  America/Argentina/Buenos\_Aires 
+  America/Noronha 
+  Atlantic/Cape\_Verde 
+  Africa/Nairobi 
+  Asia/Tehran 
+  Asia/Dubai 
+  Asia/Kabul 
+  Asia/Karachi 
+  Asia/Kolkata 
+  Asia/Kathmandu 
+  Asia/Dhaka 
+  Asia/Rangoon 
+  Asia/Bangkok 
+  Asia/Singapore 
+  Australia/Eucla 
+  Asia/Seoul 
+  Australia/Adelaide 
+  Australia/Melbourne 
+  Australia/Lord\_Howe 
+  Asia/Anadyr 
+  Pacific/Norfolk 
+  Pacific/Auckland 
+  Pacific/Chatham 
+  Pacific/Enderbury 
+  Pacific/Kiritimati 

Select a time zone from the **Other** list if items in your dataset are located within either Europe or the US, but the timestamps are standardized to a time zone outside of that region\. 

Refer to the [Joda\-Time library](http://joda-time.sourceforge.net/timezones.html) for a complete list of valid time zone names\.

You can manually set a time zone for your datasets using the Forecast console and Forecast SDK\.

------
#### [ Forecast Console ]

**To select a single time zone for your dataset**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. Choose **Create dataset group**\.

1. In **Dataset import details**, choose **Select time zone**\.

For example, use the following to apply Los Angeles time \(Pacific Standard Time\) to your datasets\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/select-timezone.PNG)

------
#### [ Forecast SDK ]

**To select a single time zone for your dataset**

Using the [ CreateDatasetImportJob](API_CreateDatasetImportJob.md) operation, set `"TimeZone"` to a valid time zone\.

For example, use the following to apply Los Angeles time \(Pacific Standard Time\) to your datasets\. 

```
{
    ...
    "TimeZone": "America/Los_Angeles"
}
```

------

## Conditions and Restrictions<a name="weather-conditions-restrictions"></a>

The following conditions and restrictions apply when using the Weather Index:
+ **Available algorithms**: You can enable the Weather Index when you train a predictor with CNN\-QR, DeepAR\+, and Prophet\. The Weather Index is not applied to ARIMA, ETS, and NPTS\.
+ **Forecast frequency**: The valid forecast frequencies are `1min`, `5min`, `10min`, `15min`, `30min`, `H` \(hourly\), `D` \(daily\)\.
+ **Forecast horizon**: The forecast horizon cannot span further than 14 days into the future\. For forecast horizon limits for each forecast frequency, refer to the list below:
  + `1min` \- 500
  + `5min` \- 500
  + `10min` \- 500
  + `15min` \- 500
  + `H` \(hourly\) \- 330
  + `D` \(daily\) \- 14
+ **Time series length**: When training a model with the Weather Index, Forecast will truncate all time series datasets to the start dates of our weather dataset featurizations\. The start dates are:
  + **US region**: July 1, 2018
  + **Europe region**: March 17, 2019
+ **Number of locations**: The target time series dataset must be limited to 2000 unique locations\.
+ **US or Europe Locations**: All items in your datasets must be located within the US \(excluding Hawaii and Alaska\) or Europe\. The latitude and longitude bounds for each region are:
  + **US region**: latitude \(24\.6, 50\.0\), longitude \(\-126\.0, \-66\.4\)
  + **Europe region**: latitude \(34\.8, 71\.8\), longitude \(\-12\.6, \-44\.8\)
+ **Minimum time series length**: Due to additional data requirements when testing the Weather Index, the minimum length for a time series dataset is: 

  `3 × ForecastHorizon + (BacktestWindows + 1) × BacktestWindowOffset`

  If your time series datasets do not meet this requirement, consider decreasing the following:
  + `ForecastHorizon` \- Shorten your forecast horizon\.
  + `BacktestWindowOffset` \- Shorten the length of the testing set during backtesting\.
  + `BacktestWindows` \- Reduce the number of backtests\.