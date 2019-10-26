# CUSTOM Domain<a name="custom-domain"></a>

The CUSTOM domain supports the following dataset types\. For each dataset type, we list required and optional fields\. For information on how to map the fields to columns in your training data, see [Dataset Domains and Dataset Types](howitworks-datasets-groups.md#howitworks-dataset-domainstypes)\.

**Topics**
+ [TARGET\_TIME\_SERIES Dataset Type](#target-time-series-type-custom-domain)
+ [RELATED\_TIME\_SERIES Dataset Type](#related-time-series-type-custom-domain)
+ [ITEM\_METADATA Dataset Type](#item-metadata-type-custom-domain)

## TARGET\_TIME\_SERIES Dataset Type<a name="target-time-series-type-custom-domain"></a>

The following fields are required: 
+ `item_id ` \(string\)
+ `timestamp` \(timestamp\)
+ `target_value` \(floating\-point integer\) – This is the `target` field for which Amazon Forecast generates a forecast\.

Ideally, only these required fields should be included\. Other additional time series information should be included in a RELATED\_TIME\_SERIES dataset\.

## RELATED\_TIME\_SERIES Dataset Type<a name="related-time-series-type-custom-domain"></a>

The following fields are required: : 
+ `item_id` \(string\)
+ `timestamp` \(timestamp\)

In addition to the required fields, your training data can include other fields\. 

## ITEM\_METADATA Dataset Type<a name="item-metadata-type-custom-domain"></a>

The following field is required: 
+ `item_id` \(string\)

Although the following field is optional, Amazon Forecast suggests that you include it:
+ `category` \(string\)

In addition to the required and suggested optional fields, your training data can include other fields\. 