# METRICS Domain<a name="metrics-domain"></a>

Use the METRICS domain for forecasting metrics, such as revenue, sales, and cash flow\. It supports the following dataset types\. For each dataset type, we list required and optional fields\. For information on how to map the fields to columns in your training data, see [Dataset Domains and Dataset Types](howitworks-datasets-groups.md#howitworks-dataset-domainstypes)\.

**Topics**
+ [TARGET\_TIME\_SERIES Dataset Type](#target-time-series-type-metrics-domain)
+ [RELATED\_TIME\_SERIES Dataset Type](#related-time-series-type-metrics-domain)
+ [ITEM\_METADATA Dataset Type](#item-metadata-type-metrics-domain)

## TARGET\_TIME\_SERIES Dataset Type<a name="target-time-series-type-metrics-domain"></a>

The following fields are required: 
+ `metric_name` \(string\)
+ `timestamp` \(timestamp\)
+ `metric_value` \(floating\-point integer\) – This is the `target` field for which Amazon Forecast generates a forecast \(for example, the amount of revenue generated on a particular day\)\.

Ideally, only these required fields should be included\. Other additional time series information should be included in a RELATED\_TIME\_SERIES dataset\.

## RELATED\_TIME\_SERIES Dataset Type<a name="related-time-series-type-metrics-domain"></a>

The following fields are required: 
+ `metric_name` \(string\)
+ `timestamp` \(timestamp\)

In addition to the required fields, your training data can include other fields\. To include other fields in the dataset, provide the fields in a schema when you create the dataset\.

## ITEM\_METADATA Dataset Type<a name="item-metadata-type-metrics-domain"></a>

The following field is required: 
+ `metric_name` \(string\)

Although the following field is optional, Amazon Forecast suggests that you include it:
+ `category` \(string\)

In addition to the required and suggested optional fields, your training data can include other fields\. To include other fields in the dataset, provide the fields in a schema when you create the dataset\.