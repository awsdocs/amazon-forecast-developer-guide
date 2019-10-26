# Predefined Dataset Domains and Dataset Types<a name="howitworks-domains-ds-types"></a>

To train a predictor, you create one or more datasets, add them to a dataset group, and provide the dataset group for training\.

For each dataset that you create, you associate a dataset domain and a dataset type\. A *dataset domain* defines a forecasting use case\.

Amazon Forecast supports the following dataset domains:
+ [RETAIL Domain](retail-domain.md) – For retail demand forecasting
+ [INVENTORY\_PLANNING Domain](inv-planning-domain.md) – For supply chain and inventory planning
+ [EC2 CAPACITY Domain](ec2-capacity-domain.md) – For forecasting Amazon Elastic Compute Cloud \(Amazon EC2\) capacity 
+ [WORK\_FORCE Domain](workforce-domain.md) – For work force planning 
+ [WEB\_TRAFFIC Domain](webtraffic-domain.md) – For estimating future web traffic 
+ [METRICS Domain](metrics-domain.md) – For forecasting metrics, such as revenue and cash flow
+ [CUSTOM Domain](custom-domain.md) – For all other types of time\-series forecasting

Each domain can have one to three *dataset types*\. The dataset types that you create for a domain are based on the type of data that you have and what you want to include in training\.

Each domain requires a `TARGET_TIME_SERIES` dataset, and optionally supports the `RELATED_TIME_SERIES` and `ITEM_METADATA` dataset types\.

The dataset types are:
+ TARGET\_TIME\_SERIES – The only required dataset type\. This type defines the *target* field that you want to generate forecasts for\. For example, if you want to forecast the sales for a set of products, then you must create a dataset of historical time\-series data for each of the products that you want to forecast\. Similarly, you can create a target\_time\_series dataset for metrics— such as revenue, cash flow, and sales—that you might want to forecast\.
+ RELATED\_TIME\_SERIES – Time\-series data that is related to the target time\-series data\. For example, price is related to product sales data, so you might provide it as a related\_time\_series\.
+ ITEM\_METADATA – Metadata that is applicable to the target time\-series data\. For example, if you are forecasting sales for a particular product, attributes of the product—such as brand, color, and genre—will be part of item\_metadata\. When predicting EC2 capacity for EC2 instances, metadata might include the CPU and memory of the instance types\.

For each dataset type, your input data must contain certain required fields\. You can also include optional fields that Amazon Forecast suggests that you include\.

The following examples show how to choose a dataset domain and corresponding dataset types\.

**Example Example 1: Dataset Types in the RETAIL Domain**  
If you are a retailer interested in forecasting demand for items, you might create the following datasets in the RETAIL domain:  
+ TARGET\_TIME\_SERIES is the required dataset of historical time\-series demand \(sales\) data for each item \(each product a retailer sells\)\. In the RETAIL domain, this dataset type requires that the dataset includes the `item_id`, `timestamp`, and the `demand` fields\. The `demand` field is the forecast target, and is typically the number of items sold by the retailer in a particular week or day\.
+ Optionally, a dataset of the RELATED\_TIME\_SERIES type\. In the RETAIL domain, this type can include optional, but suggested, time\-series information such as `price`, `inventory_onhand`, `in_stock`, and `webpage_hits`\.
+ Optionally, a dataset of the ITEM\_METADATA type\. In the RETAIL domain, Amazon Forecast suggests providing metadata information related to the items that you provided in TARGET\_TIME\_SERIES, such as `brand`, `color`, `category`, and `genre`\.

**Example Example 2: Dataset Types in the METRICS Domain**  
If you want to forecast key metrics for your organization—such as revenue, sales and cash flow—you can provide Amazon Forecast with the following datasets:  
+ The TARGET\_TIME\_SERIES dataset that provides historical time\-series data for the metric that you want to forecast\. If your interest is to forecast the revenue of all of the business units in your organization, you can create a `target_time_series` dataset with the `metric`, `business unit`, and `metric_value` fields\.
+ If you have any metadata for each metric that isn't required, such as `category` or `location`, you might provide datasets of the RELATED\_TIME\_SERIES and ITEM\_METADATA type\.
You can provide only the TARGET\_TIME\_SERIES dataset to Amazon Forecast and generate forecasts for your target metrics\. 

**Example Example 3: Dataset Types in the CUSTOM Domain**  
The training data for your forecasting application might not fit into any of the Amazon Forecast domains\. If that's the case, choose the CUSTOM domain\. You must provide the TARGET\_TIME\_SERIES dataset, but you can add your own custom fields\.  
The [Getting Started](getting-started.md) exercise forecasts electricity usage for a client\. The electricity usage training data doesn't fit into any of the dataset domains, so we used the CUSTOM domain\. In the exercise, we use only one dataset type, the TARGET\_TIME\_SERIES type\. We map the data fields to the minimum fields required by the dataset type\.