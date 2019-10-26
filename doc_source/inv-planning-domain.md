# INVENTORY\_PLANNING Domain<a name="inv-planning-domain"></a>

Use the INVENTORY\_PLANNING domain for forecasting demand for raw materials and determining how much inventory of a particular item to stock\. It supports the following dataset types\. For each dataset type, we list required and optional fields\. For information on how to map the fields to columns in your training data, see [Dataset Domains and Dataset Types](howitworks-datasets-groups.md#howitworks-dataset-domainstypes)\.

**Topics**
+ [TARGET\_TIME\_SERIES Dataset Type](#target-time-series-type-inv-planning-domain)
+ [RELATED\_TIME\_SERIES Dataset Type](#related-time-series-type-related_time_series-domain)
+ [ITEM\_METADATA Dataset Type](#item-metadata-type-related_time_series-domain)

## TARGET\_TIME\_SERIES Dataset Type<a name="target-time-series-type-inv-planning-domain"></a>

The following fields are required: 
+ `item_id` \(string\)
+ `timestamp` \(timestamp\)
+ `demand` \(float\) – This is the `target` field for which Amazon Forecast generates a forecast\.

Although the following field is optional, Amazon Forecast suggests that you include it:
+ `location` \(string\) – The location of the distribution center where the item is stocked\.

Ideally, only these required and suggested optional fields should be included\. Other additional time series information should be included in a RELATED\_TIME\_SERIES dataset\.

## RELATED\_TIME\_SERIES Dataset Type<a name="related-time-series-type-related_time_series-domain"></a>

The following fields are required: 
+ `item_id` \(string\)
+ `timestamp` \(timestamp\)

Although the following fields are optional, Amazon Forecast suggests that you include them:
+ `price` \(float\) – The price of the item 
+ `stockout_days` \(float\) – The number of days until the item will go out of stock\.
+ `inventory_onhand` \(float\) – The number of items left in stock\.
+ `revenue` \(float\) – The revenue produced from sales of the item\.
+ `in_stock` \(integer; 1=true; 0=false\) – Whether the item was in stock or not\.

In addition to the required and suggested optional fields, your training data can include other fields\. To include other fields in the dataset, provide the fields in a schema when you create the dataset\.

## ITEM\_METADATA Dataset Type<a name="item-metadata-type-related_time_series-domain"></a>

The following fields are required: 
+ `item_id` \(string\)

Although the following fields are optional, Amazon Forecast suggests that you include them:
+ `category` \(string\) – The category of the item\.
+ `brand` \(string\) – The brand of the item\.
+ `lead_time` \(string\) – The lead time, in days, to manufacture the item\.
+ `order_cycle` \(string\) – The order cycle starts when work begins and ends when the item is ready for delivery\.
+ `safety_stock` \(string\) – The minimum amount of stock to keep on hand for that item\.

In addition to the required and suggested optional fields, your training data can include other fields\. To include other fields in the dataset, provide the fields in a schema when you create the dataset\.