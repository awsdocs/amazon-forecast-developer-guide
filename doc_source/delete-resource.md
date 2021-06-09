# Deleting Resources<a name="delete-resource"></a>

You can delete individual Amazon Forecast resources and entire resource trees with the Amazon Forecast console and AWS Software Development Kit \(SDK\)\. 

A Forecast resource tree is a parent\-child hierarchical structure\. *Child resources* are resources created from other resources\. For example, when you create a predictor using a dataset group, the dataset group is the parent resource and the predictor is the child resource\. When deleting a Forecast resource, you must also delete its child resources\.

Deleting a resource or resource tree is an irreversible action\. It can't be stopped after it begins

**Topics**
+ [Understanding Resource Trees](#understanding-resource-trees)
+ [Deleting Individual Resources](#deleting-resources)
+ [Deleting Resource Trees](#deleting-resource-trees)

## Understanding Resource Trees<a name="understanding-resource-trees"></a>

The Forecast resource tree is a parent\-child hierarchical structure\. *Child resources* are resources that were created from another resource\. For example, when a forecast is generated from a predictor, the forecast is the child resource and the predictor is the parent resource\. 

To delete a Forecast resource, you must also delete its entire resource tree\. This includes all child resources of the parent resource, and also the child resources of those child resources\. 

**Note**  
Deleting a resource tree deletes only Amazon Forecast resources\. It doesn't delete datasets or exported files stored in Amazon Simple Storage Service \(Amazon S3\)\.

Forecast resources have the following parent\-child resource hierarchies\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/resource-tree.jpg)

For example, the resource tree of a *predictor* includes *predictor backtest jobs*, *forecasts*, and *forecast export jobs* as child resources\. The resource tree of a *forecast* includes only *forecast export jobs* as child resources\.

The *dataset* resource tree includes *dataset import jobs* as a child resource\. Neither *datsets* or *dataset import jobs* are part of the *dataset group* resource tree\.


| Parent Resource | Child Resources | 
| --- | --- | 
| Dataset | Dataset import jobs | 
| Dataset group | Predictors, predictor backtest export jobs, forecasts, forecast export jobs | 
| Predictor | Predictor backtest export jobs, forecasts, forecast export jobs | 
| Forecast |  Forecast export jobs  | 

If a resource doesn't have any child resources, you can delete it individually\. If a resource has child resources, you must delete the entire resource tree\. 

When using the Forecast console, you are automatically prompted to delete the entire resource tree when you delete a resource with child resources\. When using the AWS Software Development Kit \(SDK\), use the [DeleteResourceTree](API_DeleteResourceTree.md) operation to delete a resource tree\.

## Deleting Individual Resources<a name="deleting-resources"></a>

You can delete an individual resource if it's not associated with any child resources\. For example, you can delete an individual predictor that has not been used to create any forecasts or export jobs\. 

You can delete resources using the Amazon Forecast console or the AWS Software Development Kit \(SDK\)\.

------
#### [ Console ]

**To delete a resource**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. In the navigation pane, choose the resource type of the resource that you want to delete\.

1. Choose the resource and choose **Delete**\.

1. In the confirmation field, type **delete**\.

1. Choose **Delete**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/resource-delete.PNG)

------
#### [ SDK ]

**To delete a resource**

The operation that you use to delete a resource depends on its resource type\. Specify the resource Amazon Resource Name \(ARN\) in the operation for the resource type the you want to delete:
+ [DeleteDataset](API_DeleteDataset.md)
+ [DeleteDatasetGroup](API_DeleteDatasetGroup.md)
+ [DeleteDatasetImportJob](API_DeleteDatasetImportJob.md)
+ [DeletePredictor](API_DeletePredictor.md)
+ [DeletePredictorBacktestExportJob](API_DeletePredictorBacktestExportJob.md)
+ [DeleteForecast](API_DeleteForecast.md)
+ [DeleteForecastExportJob](API_DeleteForecastExportJob.md)

For example, to delete a predictor with the [DeletePredictor](API_DeletePredictor.md) operation, specify the value of `PredictorArn` to the ARN of the predictor that you want to delete\.

```
        { 
            "PredictorArn": arn:partition:service:region:account-id:resource-id
        }
```

------

## Deleting Resource Trees<a name="deleting-resource-trees"></a>

Deleting a resource tree deletes the parent resource and all associated child resources\. For example, you can delete a predictor and all child resources — predictor backtest export jobs, forecasts, and forecast export jobs — associated with the predictor\. You delete a resource tree by specifying the parent resource\. 

 You can delete resource trees using the Amazon Forecast console or the AWS Software Development Kit \(SDK\)\. 

------
#### [ Console ]

**To delete a resource tree**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. In the navigation pane, choose the resource type of the parent resource\.

1. Choose the parent resource that you want to delete\. and choose **Delete**\.

1. In the confirmation field, type **delete**\.

1. Choose **Delete**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/forecast/latest/dg/images/resource-tree-delete.PNG)

------
#### [ SDK ]

**To delete a resource tree**

To delete a resource tree, use the [DeleteResourceTree](API_DeleteResourceTree.md) operation\. Set the value of `ResourceArn` to the Amazon Resource Name \(ARN\) of the parent resource\.

```
        { 
            "ResourceArn": arn:partition:service:region:account-id:resource-id
        }
```

------