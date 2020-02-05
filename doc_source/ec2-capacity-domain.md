# EC2 CAPACITY Domain<a name="ec2-capacity-domain"></a>

Use the EC2 CAPACITY domain for forecasting Amazon EC2 capacity\. It supports the following dataset types\. For each dataset type, we list required and optional fields\. For information on how to map the fields to columns in your training data, see [Dataset Domains and Dataset Types](howitworks-datasets-groups.md#howitworks-dataset-domainstypes)\.

## Target Time Series Dataset Type<a name="target-time-series-type-ec2-capacity-domain"></a>

The following fields are required: 
+ `instance_type` \(string\) – The type of instance \(for example, c5\.xlarge\)\.
+ `timestamp` \(timestamp\)
+ `number_of_instances` \(integer\) – The number of instances of that particular instance type that was consumed at the timestamp\. This is the `target` field for which Amazon Forecast generates a forecast\.

Although the following field is optional, Amazon Forecast suggests that you include it:
+ `location` \(string\) – You can provide an AWS Region, such as us\-west\-2 or us\-east\-1\.

Ideally, only these required and suggested optional fields should be included\. Other additional time series information should be included in a related time series dataset\.

## Related Time Series Dataset Type<a name="related-time-series-type-ec2-capacity-domain"></a>

The following fields are required: 
+ `instance_type` \(string\)
+ `timestamp` \(timestamp\)

Although the following field is optional, Amazon Forecast suggests that you include it:
+ `traffic_to_service` \(floating\-point integer\) – The amount of requests sent to that instance type at the timestamp\.

In addition to the required and suggested optional fields, your training data can include other fields\. To include other fields in the dataset, provide the fields in a schema when you create the dataset\.