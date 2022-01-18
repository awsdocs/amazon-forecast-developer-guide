# What Is Amazon Forecast?<a name="what-is-forecast"></a>

Amazon Forecast is a fully managed service that uses statistical and machine learning algorithms to deliver highly accurate time\-series forecasts\. Based on the same technology used for time\-series forecasting at Amazon\.com, Forecast provides state\-of\-the\-art algorithms to predict future time\-series data based on historical data, and requires no machine learning experience\.

Time\-series forecasting is useful in multiple fields, including retail, finance, logistics, and healthcare\. You can also use Forecast to predict domain\-specific metrics for your inventory, workforce, web traffic, server capacity, and finances\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/Forecast_HowitWorks.png)

For more information about the technical aspects of Amazon Forecast, see [Time Series Forecasting Principles with Amazon Forecast](https://d1.awsstatic.com/whitepapers/time-series-forecasting-principles-amazon-forecast.pdf?did=wp_card&trk=wp_card)\.

**Topics**
+ [Using Amazon Forecast](#whatis-uses)
+ [Features of Amazon Forecast](#whatis-features)
+ [Pricing for Amazon Forecast](#whatis-pricing)
+ [Are You a First\-Time User of Amazon Forecast?](#whatis-firsttimeuser)

## Using Amazon Forecast<a name="whatis-uses"></a>

You can use the [APIs](api-reference.md), [AWS Command Line Interface](gs-cli.md) \(AWS CLI\), [Python Software Development Kit](getting-started-python.md) \(SDK\), and [Amazon Forecast console](gs-console.md) to import time series datasets, train predictors, and generate forecasts\.

Here are some common use cases for Amazon Forecast:
+ **Retail demand planning** – Predict product demand, allowing you to more accurately vary inventory and pricing at different store locations\.
+ **Supply chain planning** – Predict the quantity of raw goods, services, or other inputs required by manufacturing\.
+ **Resource planning** – Predict requirements for staffing, advertising, energy consumption, and server capacity\.
+ **Operational planning** – Predict levels of web traffic, AWS usage, and IoT sensor usage\.

## Features of Amazon Forecast<a name="whatis-features"></a>

Amazon Forecast automates much of the time\-series forecasting process, enabling you to focus on preparing your datasets and interpretting your predictions\. 

Forecast provides the following features:
+ **Automated machine learning** – Forecast automates complex machine learning tasks by finding the optimal combination of machine learning algorithms for your datasets\.
+ **State\-of\-the\-art algorithms** – Apply a combination of machine learning algorithms that are based on the same technology used at Amazon\.com\. Forecast offers a wide range of training algorithms, from commonly used statistical methods to complex neural networks\.
+ **Missing value support** – Forecast provides several filling methods to automatically handle missing values in your datasets\.
+ **Additional built\-in datasets** – Forecast can automatically incorporate built\-in datasets to improve your model\. These datasets are already feature engineered and do not require additional configuration\.

## Pricing for Amazon Forecast<a name="whatis-pricing"></a>

 With Amazon Forecast, you pay only for what you use\. There are no minimum fees and no upfront commitments\. The costs of Amazon Forecast depend on the number generated forecasts, data storage, and training hours\.

The [AWS Free Tier](https://aws.amazon.com/free/) allows you a monthly limit of up to 10,000 time series forecasts, up to 10GB of storage, and up to 10 hours of training time\. The Amazon Forecast free tier is valid for the first two months of usage\.

For a complete list of charges and prices, see [Amazon Forecast pricing](https://aws.amazon.com/forecast/pricing/)\.

## Are You a First\-Time User of Amazon Forecast?<a name="whatis-firsttimeuser"></a>

If you are a first\-time user of Amazon Forecast, we recommend that you start with the following pages:

1. [How Amazon Forecast Works](how-it-works.md) – Learn about the key concepts and the process of importing datasets, creating predictors, and generating forecasts\.

1. [Getting Started](getting-started.md) – Follow one of the tutorials to create your first Amazon Forecast forecasting predictor\.

1.  [API Reference](api-reference.md) – Familiarize yourself with the Amazon Forecast API actions and data types\.