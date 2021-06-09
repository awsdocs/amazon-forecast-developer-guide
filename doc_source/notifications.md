# Receiving Job Status Notifications<a name="notifications"></a>

You can have Amazon EventBridge or Amazon CloudWatch Events notify you with status updates for ongoing Amazon Forecast resource jobs, such as creating predictors or forecasts\. EventBridge and CloudWatch Events deliver a near real\-time stream of system events that describe changes in Amazon Web Services \(AWS\) resources\. For example, you can set up an event to notify you when a Forecast predictor finishes training\. 

Events are emitted on a best\-effort basis\. For more information about events, see the [Amazon EventBridge User Guide](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html) or the [Amazon CloudWatch Events User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html)\.

**Note**  
We recommend using Amazon EventBridge to manage events\. CloudWatch Events and EventBridge use the same API and provide the same functionality, but EventBridge provides more features\. Changes that you make in either CloudWatch or EventBridge will appear in each console\. For more information, see [Amazon EventBridge](https://docs.aws.amazon.com/eventbridge/index.html)\.

**Topics**
+ [Monitoring Forecast Resource Jobs](#forecast-events)
+ [Creating an EventBridge Rule for Job Status Notifications](#create-rule-event-bridge)
+ [Creating a CloudWatch Events Rule for Job Status Notifications](#create-rule-cloud-watch)

## Monitoring Forecast Resource Jobs<a name="forecast-events"></a>

An event indicates a change in your AWS environment, and a rule matches incoming events and routes them to targets for processing\. You can set up rules to match Forecast events and route them to one or more target functions or streams\. EventBridge and CloudWatch Events detect events as they occur and invoke the target in the matching rule\.

The following table lists the Forecast resource jobs and their status change events, which you can monitor\.


|  Resource Job  |  Status Change Event Name  |  Status  | 
| --- | --- | --- | 
| [CreateDatasetImportJob](https://docs.aws.amazon.com/forecast/latest/dg/API_CreateDatasetImportJob.html) | Forecast Dataset Import Job State Change | ACTIVE, CREATE\_IN\_PROGRESS, CREATE\_FAILED, CREATE\_STOPPED | 
| [CreatePredictor](https://docs.aws.amazon.com/forecast/latest/dg/API_CreatePredictor.html) | Forecast Predictor Creation State Change | ACTIVE, CREATE\_IN\_PROGRESS, CREATE\_FAILED, CREATE\_STOPPED | 
| [CreateForecast](https://docs.aws.amazon.com/forecast/latest/dg/API_CreateForecast.html) | Forecast Forecast Creation State Change | ACTIVE, CREATE\_IN\_PROGRESS, CREATE\_FAILED, CREATE\_STOPPED | 
| [CreatePredictorBacktestExportJob](https://docs.aws.amazon.com/forecast/latest/dg/API_CreatePredictorBacktestExportJob.html) | Forecast Predictor Backtest Export Job State Change | ACTIVE, CREATE\_IN\_PROGRESS, CREATE\_FAILED, CREATE\_STOPPED | 
| [CreateForecastExportJob](https://docs.aws.amazon.com/forecast/latest/dg/API_CreateForecastExportJob.html) | Forecast Forecast Export Job State Change | ACTIVE, CREATE\_IN\_PROGRESS, CREATE\_FAILED, CREATE\_STOPPED | 
| [DeleteDataset](https://docs.aws.amazon.com/forecast/latest/dg/API_DeleteDataset.html) | Forecast Dataset Deletion State Change | DELETE\_IN\_PROGRESS, DELETE\_FAILED | 
| [DeleteDatasetImportJob](https://docs.aws.amazon.com/forecast/latest/dg/API_DeleteDatasetImportJob.html) | Forecast Dataset Import Job Deletion State Change | DELETE\_IN\_PROGRESS, DELETE\_FAILED | 
| [DeletePredictor](https://docs.aws.amazon.com/forecast/latest/dg/API_DeletePredictor.html) | Forecast Predictor Deletion State Change | DELETE\_IN\_PROGRESS, DELETE\_FAILED | 
| [DeleteForecast](https://docs.aws.amazon.com/forecast/latest/dg/API_DeleteForecast.html) | Forecast Forecast Deletion State Change | DELETE\_IN\_PROGRESS, DELETE\_FAILED | 

 Notifications contain information about the resource, including the Amazon Resource Name \(ARN\), job status, job duration \(in minutes\), and, if the job failed, an error message\. Delete event notifications don't include a `Duration` field\. The following is an example notification:

```
{
    "version": "0",
    "id": "017fcb6d-7ca3-ebf8-819e-3e0fa956ee17",
    "detail-type": "Forecast Dataset Import Job State Change",
    "source": "aws.forecast",
    "account": "000000000001",
    "time": "2021-02-19T05:45:51Z",
    "region": "us-east-1",
    "resources": [
        "arn:aws:forecast:us-west-2:000000000001:dataset/example_data"
    ],
    "detail": {
        "Arn": "arn:aws:forecast:us-west-2:000000000001:dataset/example_data",
        "Duration": 60,
        "Status": "ACTIVE",
    }
}
```

## Creating an EventBridge Rule for Job Status Notifications<a name="create-rule-event-bridge"></a>

To create an EventBridge rule to notify you of status changes for ongoing Forecast resource jobs, see [Creating a rule for an AWS service](https://docs.aws.amazon.com/eventbridge/latest/userguide/create-eventbridge-rule.html) in the *Amazon EventBridge User Guide*\. In the procedure, for **Service name**, choose **Amazon Forecast**\. For **Event type**, choose the Forecast event to monitor\. See [Monitoring Forecast Resource Jobs](#forecast-events) for the list of Forecast events\. 

## Creating a CloudWatch Events Rule for Job Status Notifications<a name="create-rule-cloud-watch"></a>

To create an CloudWatch Events rule to notify you of status changes for ongoing Forecast resource jobs, see [Creating a CloudWatch Events Rule That Triggers on an Event](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/Create-CloudWatch-Events-Rule.html) in the *Amazon CloudWatch User Guide*\. In the procedure, for **Service name**, choose **Amazon Forecast**\. For **Event type**, choose the Forecast event to monitor\. See [Monitoring Forecast Resource Jobs](#forecast-events) for a list of Forecast events\. 