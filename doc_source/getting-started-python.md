# Getting Started \(Python Notebooks\)<a name="getting-started-python"></a>

**Note**  
For a complete list of tutorials using Python notebooks, see the Amazon Forecast [Github Samples](https://github.com/aws-samples/amazon-forecast-samples/tree/master/notebooks) page\.

To get started using Amazon Forecast APIs with Python notebooks, see the [Basic Tutorial](https://github.com/aws-samples/amazon-forecast-samples/tree/master/notebooks/basic/Tutorial)\. The tutorial guides you through the core steps of Forecast from start to finish:

1. [Preparing data](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/basic/Tutorial/1.Getting_Data_Ready.ipynb) \- Prepare a dataset, create a dataset group, define the schema, and import the dataset group\.

1. [Training predictors](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/basic/Tutorial/2.Building_Your_Predictor.ipynb) \- Create a predictor, evaluate error metrics, and generate forecasts\.

1. [Evaluating predictors](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/basic/Tutorial/3.Evaluating_Your_Predictor.ipynb) \- Obtain predictions, visualize predictions, and compare results\.

After completing the tutorial, you can use the [Clean Up](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/basic/Tutorial/4.Cleanup.ipynb) tutorial to delete the dataset groups, predictors, forecasts created during the tutorial\.

To repeat this tutorial with AutoML, see [Getting Started with AutoML](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/advanced/Getting_started_with_AutoML/Getting_started_with_AutoML.ipynb)\.

## Advanced Tutorials<a name="getting-started-python-advanced"></a>

For more advanced tutorials, refer to the following Python notebooks:
+ [Comparing multiple models ](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/advanced/Compare_Multiple_Models/Compare_Multiple_Models.ipynb) \- Create predictors using Prophet, ETS, and DeepAR\+, and compare their performances by visualizating the results\.
+ [Cold start forecasting](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/advanced/Forecast%20with%20Cold%20Start%20Items/Forecast%20with%20Cold%20Start%20Items.ipynb) \- Use item metadata and the DeepAR\+ algorithm to forecast for cold\-start scenarios \(when there is little to no historical data\)\.
+ [Incorporating related time\-series datasets](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/advanced/Incorporating_Related_Time_Series_dataset_to_your_Predictor/Incorporating_Related_Time_Series_dataset_to_your_Predictor.ipynb) \- Use related time\-series datasets to improve the accuracy of your model\.
+ [Incorporating item metadata](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/advanced/Incorporating_Item_Metadata_Dataset_to_your_Predictor/Incorporating_Item_Metadata_Dataset_to_your_Predictor.ipynb) \- Use item metadata to improve the accuracy of your model\.
+ [Using the Weather Index](https://github.com/aws-samples/amazon-forecast-samples/tree/master/notebooks/advanced/Weather_index) \- Use the Weather Index to incorporate historical and projected weather information when training your predictors\.
+ [Performing What\-if analysis](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/advanced/WhatIf_Analysis/WhatIf_Analysis.ipynb) \- Explore different pricing scenarios and evaluate how it impacts demand\.
+ [Evaluate item\-level accuracy](https://github.com/aws-samples/amazon-forecast-samples/blob/master/notebooks/advanced/Item_Level_Accuracy/Item_Level_Accuracy_Using_Bike_Example.ipynb) \- Export backtest metrics and forecasts, and evaluate the item\-level performance of your predictor\.