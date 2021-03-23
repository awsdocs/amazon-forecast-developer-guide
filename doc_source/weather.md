# Weather Index<a name="weather"></a>

The Amazon Forecast Weather Index is a built\-in featurization that incorporates historical and projected weather information into your model\. It is especially useful for retail use cases, where temperature and precipitation can significantly affect product demand\.

When the Weather Index is enabled, Forecast applies the weather featurization only to time series where it finds improvements in accuracy during predictor training\. If supplementing a time series with weather information does not improve its predictive accuracy during backtesting, Forecast does not apply the Weather Index to that particular time series\.

To apply the Weather Index, you must include a [geolocation attribute](#adding-geolocation) in your target time series dataset and any related time series datasets\. You also need to specify [time zones](#specifying-timezones) for your target time\-series timestamps\. For more information regarding dataset requirements, see [Conditions and Restrictions](#weather-conditions-restrictions)\.

**Python notebooks**  
For a step\-by\-step guide on using the Weather Index, see [NY Taxi: Amazon Forecast with Weather Index](https://github.com/aws-samples/amazon-forecast-samples/tree/master/notebooks/advanced/Weather_index)\.

**Topics**
+ [Enabling the Weather Index](#enabling-weather)
+ [Adding Geolocation Information to Datasets](#adding-geolocation)
+ [Specifying Time Zones](#specifying-timezones)
+ [Conditions and Restrictions](#weather-conditions-restrictions)

## Enabling the Weather Index<a name="enabling-weather"></a>

The Weather Index is enabled during the predictor training stage\. It can be applied when running AutoML or manually selecting the CNN\-QR, DeepAR\+, or Prophet algorithms\. When using the [ `CreatePredictor`](API_CreatePredictor.md) operation, the Weather Index is included in the [SupplementaryFeature](API_SupplementaryFeature.md) data type\.

Before enabling the Weather Index, you must include a geolocation attribute in your target time series and related timeseries datsets, and define the time zones for your timestamps\. For more information, see [Adding Geolocation Information](#adding-geolocation) and [Specifying Time Zones](#specifying-timezones)\.

You can enable the Weather Index using the Forecast console or the Forecast Software Development Kit \(SDK\) \.

------
#### [ Console ]

**To enable the Weather Index**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. From **Dataset groups**, choose your dataset group\.

1. In the navigation pane, choose **Predictors**\.

1. Choose **Train new predictor**\.

1. Choose **Enable Weather Index**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/enable-weather.PNG)

------
#### [ SDK ]

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

## Adding Geolocation Information to Datasets<a name="adding-geolocation"></a>

To use the Weather Index, you must include a geolocation attribute for each item in your target time series and related time series datasets\. The attribute is defined with the `geolocation` attribute type within the dataset schemas\.

All geolocation values must be exclusively within either the US \(excluding Hawaii and Alaska\) or Europe region\. Your dataset cannot contain items in *both* the US and Europe\.

Specify the geolocation attribute in one of two formats:
+ **Latitude & Longitude** \(US and Europe\) \- Specify the latitude and longitude in decimal format \(Example: 47\.61\_\-122\.33\)
+ **Postal code** \(US only\) \- Specify the country code \(US\), followed by the 5\-digit ZIP code \(Example: US\_98121\)

The Latitude & Longitude format supports both the US and Europe locations\. The Postal code format only supports US locations\.

**Topics**
+ [Latitude & Longitude Bounds](#geolocation-bounds)
+ [Including Geolocation in the Dataset Schema](#geolocation-schema)
+ [Setting the Geolocation Format](#geolocation-format)

### Latitude & Longitude Bounds<a name="geolocation-bounds"></a>

The following are the latitudinal and longitudinal bounds for the US and Europe regions:

------
#### [ US Region ]

**Bounds**: latitude \(24\.6, 50\.0\), longitude \(\-126\.0, \-66\.4\)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/weather-us-bounds.png)

------
#### [ Europe Region ]

**Bounds**: latitude \(34\.8, 71\.8\), longitude \(\-12\.6, 44\.8\)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/weather-euro-bounds.png)

------

### Including Geolocation in the Dataset Schema<a name="geolocation-schema"></a>

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

### Setting the Geolocation Format<a name="geolocation-format"></a>

The format of the geolocation attribute can be in the **Postal Code** or **Latitude & Longitude** format\. You can set the geolocation format using the Forecast console or the Forecast Software Development Kit \(SDK\)\.

------
#### [ Console ]

**To add a geolocation attribute to a time series dataset**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. Choose **Create dataset group**\.

1. In the **Schema builder**, set your geolocation **Attribute type** to `geolocation`\.

1. In the **Geoloocation format** drop\-down, choose your location format\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/schema-builder-geolocation.png)

You can also define your attributes in JSON format and select a location format from the **Geolocation format** drop\-down\.

------
#### [ SDK ]

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

## Specifying Time Zones<a name="specifying-timezones"></a>

You can either let Amazon Forecast automatically synchronize your time zone information with your geolocation attribute, or you can manually assign a single time zone to your entire dataset\. 

**Topics**
+ [Automatically Sync Time Zones with Geolocation](#timezones-automatic)
+ [Manually Select a Single Time Zone](#timezones-manual)

### Automatically Sync Time Zones with Geolocation<a name="timezones-automatic"></a>

This option is ideal for datasets that contain timestamps in multiple time zones, and those timestamps are expressed in local time\. Forecast assigns a time zone for every item in the target time series dataset based on the item’s geolocation attribute\.

You can automatically sync your timestamps with your geolocation attribute using the Forecast console or Forecast SDK\.

------
#### [ Console ]

**To sync time zones with the geolocation attribute**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. In the navigation pane, choose **Create dataset group**\.

1. In **Dataset import details**, choose **Sync time zone with location**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/sync-timezone-with-geolocation.PNG)

------
#### [ SDK ]

**To sync time zones with the geolocation attribute**

Using the [ CreateDatasetImportJob](API_CreateDatasetImportJob.md) operation, set `"UseGeolocationForTimeZone"` to `"true"`\.

```
{
    ...
    "UseGeolocationForTimeZone": "true"
}
```

------

### Manually Select a Single Time Zone<a name="timezones-manual"></a>

**Note**  
You can manually select a time zone outside of the *US region* and *Europe region*\. However, all geolocation values must still be within Europe or the US\.

This option is ideal for datasets with all timestamps within a single time zone, or if all timestamps are normalized to a single time zone\. Using this option applies the same time zone to every item in the dataset\.

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

For a complete list of valid time zone names, see [Joda\-Time library](http://joda-time.sourceforge.net/timezones.html)\.

You can manually set a time zone for your datasets using the Forecast console or Forecast SDK\.

------
#### [ Console ]

**To select a single time zone for your dataset**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. In the navigation pane, choose **Create dataset group**\.

1. In **Dataset import details**, choose **Select time zone**\.

For example, use the following to apply Los Angeles time \(Pacific Standard Time\) to your datasets\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/select-timezone.PNG)

------
#### [ SDK ]

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
+ **Available algorithms**: The Weather Index can be enabled when you train a predictor with the CNN\-QR, DeepAR\+, and Prophet algorithms\. The Weather Index is not applied to ARIMA, ETS, and NPTS\.
+ **Forecast frequency**: The valid forecast frequencies are `1 minute`, `5 minutes`, `10 minutes`, `15 minutes`, `30 minutes`, `Hourly`, and `Daily`\.
+ **Forecast horizon**: The forecast horizon cannot span further than 14 days into the future\. For forecast horizon limits for each forecast frequency, refer to the list below:
  + `1 minute` \- 500
  + `5 minutes` \- 500
  + `10 minutes` \- 500
  + `15 minutes` \- 500
  + `Hourly` \- 330
  + `Daily` \- 14
+ **Time series length**: When training a model with the Weather Index, Forecast truncates all time series datasets with timestamps before July 2, 2018, which is the start date of the weather dataset featurizations\. With the Weather Index enabled, datapoints with timestamps before July 2, 2018 will not be used during predictor training\.
+ **Number of locations**: The target time series dataset cannot exceed 2000 unique locations\.
+ **US or Europe locations**: All items in your datasets must be located within the US \(excluding Hawaii and Alaska\) or Europe\. The latitudinal and longitudinal bounds are:
  + **US region**: latitude \(24\.6, 50\.0\), longitude \(\-126\.0, \-66\.4\)
  + **Europe region**: latitude \(34\.8, 71\.8\), longitude \(\-12\.6, 44\.8\)
+ **Minimum time series length**: Due to additional data requirements when testing the Weather Index, the minimum length for a time series dataset is: 

  `3 × ForecastHorizon + (BacktestWindows + 1) × BacktestWindowOffset`

  If your time series datasets do not meet this requirement, consider decreasing the following:
  + `ForecastHorizon` \- Shorten your forecast horizon\.
  + `BacktestWindowOffset` \- Shorten the length of the testing set during backtesting\.
  + `BacktestWindows` \- Reduce the number of backtests\.