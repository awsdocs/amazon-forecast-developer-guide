# GetAccuracyMetrics<a name="API_GetAccuracyMetrics"></a>

Provides metrics on the accuracy of the models that were trained by the [CreatePredictor](API_CreatePredictor.md) operation\. Use metrics to see how well the model performed and to decide whether to use the predictor to generate a forecast\. For more information, see [Predictor Metrics](https://docs.aws.amazon.com/forecast/latest/dg/metrics.html)\.

This operation generates metrics for each backtest window that was evaluated\. The number of backtest windows \(`NumberOfBacktestWindows`\) is specified using the [EvaluationParameters](API_EvaluationParameters.md) object, which is optionally included in the `CreatePredictor` request\. If `NumberOfBacktestWindows` isn't specified, the number defaults to one\.

The parameters of the `filling` method determine which items contribute to the metrics\. If you want all items to contribute, specify `zero`\. If you want only those items that have complete data in the range being evaluated to contribute, specify `nan`\. For more information, see [FeaturizationMethod](API_FeaturizationMethod.md)\.

**Note**  
Before you can get accuracy metrics, the `Status` of the predictor must be `ACTIVE`, signifying that training has completed\. To get the status, use the [DescribePredictor](API_DescribePredictor.md) operation\.

## Request Syntax<a name="API_GetAccuracyMetrics_RequestSyntax"></a>

```
{
   "PredictorArn": "string"
}
```

## Request Parameters<a name="API_GetAccuracyMetrics_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [PredictorArn](#API_GetAccuracyMetrics_RequestSyntax) **   <a name="forecast-GetAccuracyMetrics-request-PredictorArn"></a>
The Amazon Resource Name \(ARN\) of the predictor to get metrics for\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: Yes

## Response Syntax<a name="API_GetAccuracyMetrics_ResponseSyntax"></a>

```
{
   "AutoMLOverrideStrategy": "string",
   "IsAutoPredictor": boolean,
   "OptimizationMetric": "string",
   "PredictorEvaluationResults": [ 
      { 
         "AlgorithmArn": "string",
         "TestWindows": [ 
            { 
               "EvaluationType": "string",
               "ItemCount": number,
               "Metrics": { 
                  "AverageWeightedQuantileLoss": number,
                  "ErrorMetrics": [ 
                     { 
                        "ForecastType": "string",
                        "MAPE": number,
                        "MASE": number,
                        "RMSE": number,
                        "WAPE": number
                     }
                  ],
                  "RMSE": number,
                  "WeightedQuantileLosses": [ 
                     { 
                        "LossValue": number,
                        "Quantile": number
                     }
                  ]
               },
               "TestWindowEnd": number,
               "TestWindowStart": number
            }
         ]
      }
   ]
}
```

## Response Elements<a name="API_GetAccuracyMetrics_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AutoMLOverrideStrategy](#API_GetAccuracyMetrics_ResponseSyntax) **   <a name="forecast-GetAccuracyMetrics-response-AutoMLOverrideStrategy"></a>
 The `LatencyOptimized` AutoML override strategy is only available in private beta\. Contact AWS Support or your account manager to learn more about access privileges\. 
The AutoML strategy used to train the predictor\. Unless `LatencyOptimized` is specified, the AutoML strategy optimizes predictor accuracy\.  
This parameter is only valid for predictors trained using AutoML\.  
Type: String  
Valid Values:` LatencyOptimized | AccuracyOptimized` 

 ** [IsAutoPredictor](#API_GetAccuracyMetrics_ResponseSyntax) **   <a name="forecast-GetAccuracyMetrics-response-IsAutoPredictor"></a>
Whether the predictor was created with [CreateAutoPredictor](API_CreateAutoPredictor.md)\.  
Type: Boolean

 ** [OptimizationMetric](#API_GetAccuracyMetrics_ResponseSyntax) **   <a name="forecast-GetAccuracyMetrics-response-OptimizationMetric"></a>
The accuracy metric used to optimize the predictor\.  
Type: String  
Valid Values:` WAPE | RMSE | AverageWeightedQuantileLoss | MASE | MAPE` 

 ** [PredictorEvaluationResults](#API_GetAccuracyMetrics_ResponseSyntax) **   <a name="forecast-GetAccuracyMetrics-response-PredictorEvaluationResults"></a>
An array of results from evaluating the predictor\.  
Type: Array of [EvaluationResult](API_EvaluationResult.md) objects

## Errors<a name="API_GetAccuracyMetrics_Errors"></a>

 ** InvalidInputException **   
We can't process the request because it includes an invalid value or a value that exceeds the valid range\.  
HTTP Status Code: 400

 ** ResourceInUseException **   
The specified resource is in use\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
We can't find a resource with that Amazon Resource Name \(ARN\)\. Check the ARN and try again\.  
HTTP Status Code: 400

## See Also<a name="API_GetAccuracyMetrics_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/GetAccuracyMetrics) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/GetAccuracyMetrics) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/GetAccuracyMetrics) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/GetAccuracyMetrics) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/forecast-2018-06-26/GetAccuracyMetrics) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/GetAccuracyMetrics) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/GetAccuracyMetrics) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/GetAccuracyMetrics) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/forecast-2018-06-26/GetAccuracyMetrics) 