# WORK\_FORCE Domain<a name="workforce-domain"></a>

Use the WORK\_FORCE domain to forecast workforce demand\. It supports the following dataset types\. For each dataset type, we list required and optional fields\. For information on how to map the fields to columns in your training data, see [Dataset Domains and Dataset Types](howitworks-datasets-groups.md#howitworks-dataset-domainstypes)\.

**Topics**
+ [TARGET\_TIME\_SERIES Dataset Type](#target-time-series-type-workforce-domain)
+ [RELATED\_TIME\_SERIES Dataset Type](#related-time-series-type-workforce-domain)
+ [ITEM\_METADATA Dataset Type](#item-metadata-type-workforce-domain)

## TARGET\_TIME\_SERIES Dataset Type<a name="target-time-series-type-workforce-domain"></a>

The following fields are required: 
+ `workforce_type` \(string\) – The type of work force labor being forecast\. For example, call center demand or fulfillment center labor demand\.
+ `timestamp` \(timestamp\)
+ `workforce_demand` \(floating\-point integer\) – This is the `target` field for which Amazon Forecast generates a forecast\.

Although the following field is optional, Amazon Forecast suggests that you include it:
+ `location` \(string\) – The location where the work force resources are sought\.

Ideally, only these required and suggested optional fields should be included\. Other additional time series information should be included in a RELATED\_TIME\_SERIES dataset\.

## RELATED\_TIME\_SERIES Dataset Type<a name="related-time-series-type-workforce-domain"></a>

The following fields are required: 
+ `workforce_type` \(string\)
+ `timestamp` \(timestamp\)

In addition to the required fields, your training data can include other fields\. To include other fields in the dataset, provide the fields in a schema when you create the dataset\.

## ITEM\_METADATA Dataset Type<a name="item-metadata-type-workforce-domain"></a>

The following field is required: 
+ `workforce_type` \(string\)

Although the following fields are optional, Amazon Forecast suggests that you include them:
+ `wages` \(float\) – The average wages for that particular workforce type\.
+ `shift_length` \(string\) – The length of the shift\.
+ `location` \(string\) – The location of the workforce\.

In addition to the required and suggested optional fields, your training data can include other fields\. To include other fields in the dataset, provide the fields in a schema when you create the dataset\.