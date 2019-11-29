# DescribePredictor<a name="API_DescribePredictor"></a>

Describes a predictor created using the [CreatePredictor](API_CreatePredictor.md) operation\.

In addition to listing the properties provided in the `CreatePredictor` request, this operation lists the following properties:
+  `DatasetImportJobArns` \- The dataset import jobs used to import training data\.
+  `AutoMLAlgorithmArns` \- If AutoML is performed, the algorithms that were evaluated\.
+  `CreationTime` 
+  `LastModificationTime` 
+  `Status` 
+  `Message` \- If an error occurred, information about the error\.

## Request Syntax<a name="API_DescribePredictor_RequestSyntax"></a>

```
{
   "[PredictorArn](#forecast-DescribePredictor-request-PredictorArn)": "string"
}
```

## Request Parameters<a name="API_DescribePredictor_RequestParameters"></a>

The request accepts the following data in JSON format\.

 ** [PredictorArn](#API_DescribePredictor_RequestSyntax) **   <a name="forecast-DescribePredictor-request-PredictorArn"></a>
The Amazon Resource Name \(ARN\) of the predictor that you want information about\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$`   
Required: Yes

## Response Syntax<a name="API_DescribePredictor_ResponseSyntax"></a>

```
{
   "[AlgorithmArn](#forecast-DescribePredictor-response-AlgorithmArn)": "string",
   "[AutoMLAlgorithmArns](#forecast-DescribePredictor-response-AutoMLAlgorithmArns)": [ "string" ],
   "[CreationTime](#forecast-DescribePredictor-response-CreationTime)": number,
   "[DatasetImportJobArns](#forecast-DescribePredictor-response-DatasetImportJobArns)": [ "string" ],
   "[EncryptionConfig](#forecast-DescribePredictor-response-EncryptionConfig)": { 
      "[KMSKeyArn](API_EncryptionConfig.md#forecast-Type-EncryptionConfig-KMSKeyArn)": "string",
      "[RoleArn](API_EncryptionConfig.md#forecast-Type-EncryptionConfig-RoleArn)": "string"
   },
   "[EvaluationParameters](#forecast-DescribePredictor-response-EvaluationParameters)": { 
      "[BackTestWindowOffset](API_EvaluationParameters.md#forecast-Type-EvaluationParameters-BackTestWindowOffset)": number,
      "[NumberOfBacktestWindows](API_EvaluationParameters.md#forecast-Type-EvaluationParameters-NumberOfBacktestWindows)": number
   },
   "[FeaturizationConfig](#forecast-DescribePredictor-response-FeaturizationConfig)": { 
      "[Featurizations](API_FeaturizationConfig.md#forecast-Type-FeaturizationConfig-Featurizations)": [ 
         { 
            "[AttributeName](API_Featurization.md#forecast-Type-Featurization-AttributeName)": "string",
            "[FeaturizationPipeline](API_Featurization.md#forecast-Type-Featurization-FeaturizationPipeline)": [ 
               { 
                  "[FeaturizationMethodName](API_FeaturizationMethod.md#forecast-Type-FeaturizationMethod-FeaturizationMethodName)": "string",
                  "[FeaturizationMethodParameters](API_FeaturizationMethod.md#forecast-Type-FeaturizationMethod-FeaturizationMethodParameters)": { 
                     "string" : "string" 
                  }
               }
            ]
         }
      ],
      "[ForecastDimensions](API_FeaturizationConfig.md#forecast-Type-FeaturizationConfig-ForecastDimensions)": [ "string" ],
      "[ForecastFrequency](API_FeaturizationConfig.md#forecast-Type-FeaturizationConfig-ForecastFrequency)": "string"
   },
   "[ForecastHorizon](#forecast-DescribePredictor-response-ForecastHorizon)": number,
   "[HPOConfig](#forecast-DescribePredictor-response-HPOConfig)": { 
      "[ParameterRanges](API_HyperParameterTuningJobConfig.md#forecast-Type-HyperParameterTuningJobConfig-ParameterRanges)": { 
         "[CategoricalParameterRanges](API_ParameterRanges.md#forecast-Type-ParameterRanges-CategoricalParameterRanges)": [ 
            { 
               "[Name](API_CategoricalParameterRange.md#forecast-Type-CategoricalParameterRange-Name)": "string",
               "[Values](API_CategoricalParameterRange.md#forecast-Type-CategoricalParameterRange-Values)": [ "string" ]
            }
         ],
         "[ContinuousParameterRanges](API_ParameterRanges.md#forecast-Type-ParameterRanges-ContinuousParameterRanges)": [ 
            { 
               "[MaxValue](API_ContinuousParameterRange.md#forecast-Type-ContinuousParameterRange-MaxValue)": number,
               "[MinValue](API_ContinuousParameterRange.md#forecast-Type-ContinuousParameterRange-MinValue)": number,
               "[Name](API_ContinuousParameterRange.md#forecast-Type-ContinuousParameterRange-Name)": "string",
               "[ScalingType](API_ContinuousParameterRange.md#forecast-Type-ContinuousParameterRange-ScalingType)": "string"
            }
         ],
         "[IntegerParameterRanges](API_ParameterRanges.md#forecast-Type-ParameterRanges-IntegerParameterRanges)": [ 
            { 
               "[MaxValue](API_IntegerParameterRange.md#forecast-Type-IntegerParameterRange-MaxValue)": number,
               "[MinValue](API_IntegerParameterRange.md#forecast-Type-IntegerParameterRange-MinValue)": number,
               "[Name](API_IntegerParameterRange.md#forecast-Type-IntegerParameterRange-Name)": "string",
               "[ScalingType](API_IntegerParameterRange.md#forecast-Type-IntegerParameterRange-ScalingType)": "string"
            }
         ]
      }
   },
   "[InputDataConfig](#forecast-DescribePredictor-response-InputDataConfig)": { 
      "[DatasetGroupArn](API_InputDataConfig.md#forecast-Type-InputDataConfig-DatasetGroupArn)": "string",
      "[SupplementaryFeatures](API_InputDataConfig.md#forecast-Type-InputDataConfig-SupplementaryFeatures)": [ 
         { 
            "[Name](API_SupplementaryFeature.md#forecast-Type-SupplementaryFeature-Name)": "string",
            "[Value](API_SupplementaryFeature.md#forecast-Type-SupplementaryFeature-Value)": "string"
         }
      ]
   },
   "[LastModificationTime](#forecast-DescribePredictor-response-LastModificationTime)": number,
   "[Message](#forecast-DescribePredictor-response-Message)": "string",
   "[PerformAutoML](#forecast-DescribePredictor-response-PerformAutoML)": boolean,
   "[PerformHPO](#forecast-DescribePredictor-response-PerformHPO)": boolean,
   "[PredictorArn](#forecast-DescribePredictor-response-PredictorArn)": "string",
   "[PredictorExecutionDetails](#forecast-DescribePredictor-response-PredictorExecutionDetails)": { 
      "[PredictorExecutions](API_PredictorExecutionDetails.md#forecast-Type-PredictorExecutionDetails-PredictorExecutions)": [ 
         { 
            "[AlgorithmArn](API_PredictorExecution.md#forecast-Type-PredictorExecution-AlgorithmArn)": "string",
            "[TestWindows](API_PredictorExecution.md#forecast-Type-PredictorExecution-TestWindows)": [ 
               { 
                  "[Message](API_TestWindowSummary.md#forecast-Type-TestWindowSummary-Message)": "string",
                  "[Status](API_TestWindowSummary.md#forecast-Type-TestWindowSummary-Status)": "string",
                  "[TestWindowEnd](API_TestWindowSummary.md#forecast-Type-TestWindowSummary-TestWindowEnd)": number,
                  "[TestWindowStart](API_TestWindowSummary.md#forecast-Type-TestWindowSummary-TestWindowStart)": number
               }
            ]
         }
      ]
   },
   "[PredictorName](#forecast-DescribePredictor-response-PredictorName)": "string",
   "[Status](#forecast-DescribePredictor-response-Status)": "string",
   "[TrainingParameters](#forecast-DescribePredictor-response-TrainingParameters)": { 
      "string" : "string" 
   }
}
```

## Response Elements<a name="API_DescribePredictor_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AlgorithmArn](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-AlgorithmArn"></a>
The Amazon Resource Name \(ARN\) of the algorithm used for model training\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

 ** [AutoMLAlgorithmArns](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-AutoMLAlgorithmArns"></a>
When `PerformAutoML` is specified, the ARN of the chosen algorithm\.  
Type: Array of strings  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

 ** [CreationTime](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-CreationTime"></a>
When the model training task was created\.  
Type: Timestamp

 ** [DatasetImportJobArns](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-DatasetImportJobArns"></a>
An array of the ARNs of the dataset import jobs used to import training data for the predictor\.  
Type: Array of strings  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\-\_\.\/\:]+$` 

 ** [EncryptionConfig](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-EncryptionConfig"></a>
An AWS Key Management Service \(KMS\) key and the AWS Identity and Access Management \(IAM\) role that Amazon Forecast can assume to access the key\.  
Type: [EncryptionConfig](API_EncryptionConfig.md) object

 ** [EvaluationParameters](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-EvaluationParameters"></a>
Used to override the default evaluation parameters of the specified algorithm\. Amazon Forecast evaluates a predictor by splitting a dataset into training data and testing data\. The evaluation parameters define how to perform the split and the number of iterations\.  
Type: [EvaluationParameters](API_EvaluationParameters.md) object

 ** [FeaturizationConfig](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-FeaturizationConfig"></a>
The featurization configuration\.  
Type: [FeaturizationConfig](API_FeaturizationConfig.md) object

 ** [ForecastHorizon](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-ForecastHorizon"></a>
The number of time\-steps of the forecast\. The forecast horizon is also called the prediction length\.  
Type: Integer

 ** [HPOConfig](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-HPOConfig"></a>
The hyperparameter override values for the algorithm\.  
Type: [HyperParameterTuningJobConfig](API_HyperParameterTuningJobConfig.md) object

 ** [InputDataConfig](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-InputDataConfig"></a>
Describes the dataset group that contains the data to use to train the predictor\.  
Type: [InputDataConfig](API_InputDataConfig.md) object

 ** [LastModificationTime](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-LastModificationTime"></a>
Initially, the same as `CreationTime` \(when the status is `CREATE_PENDING`\)\. This value is updated when training starts \(when the status changes to `CREATE_IN_PROGRESS`\), and when training has completed \(when the status changes to `ACTIVE`\) or fails \(when the status changes to `CREATE_FAILED`\)\.  
Type: Timestamp

 ** [Message](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-Message"></a>
If an error occurred, an informational message about the error\.  
Type: String

 ** [PerformAutoML](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-PerformAutoML"></a>
Whether the predictor is set to perform AutoML\.  
Type: Boolean

 ** [PerformHPO](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-PerformHPO"></a>
Whether the predictor is set to perform hyperparameter optimization \(HPO\)\.  
Type: Boolean

 ** [PredictorArn](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-PredictorArn"></a>
The ARN of the predictor\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*` 

 ** [PredictorExecutionDetails](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-PredictorExecutionDetails"></a>
Details on the the status and results of the backtests performed to evaluate the accuracy of the predictor\. You specify the number of backtests to perform when you call the [CreatePredictor](API_CreatePredictor.md) operation\.  
Type: [PredictorExecutionDetails](API_PredictorExecutionDetails.md) object

 ** [PredictorName](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-PredictorName"></a>
The name of the predictor\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_]*` 

 ** [Status](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-Status"></a>
The status of the predictor\. States include:  
+  `ACTIVE` 
+  `CREATE_PENDING`, `CREATE_IN_PROGRESS`, `CREATE_FAILED` 
+  `DELETE_PENDING`, `DELETE_IN_PROGRESS`, `DELETE_FAILED` 
+  `UPDATE_PENDING`, `UPDATE_IN_PROGRESS`, `UPDATE_FAILED` 
The `Status` of the predictor must be `ACTIVE` before you can use the predictor to create a forecast\.
Type: String  
Length Constraints: Maximum length of 256\.

 ** [TrainingParameters](#API_DescribePredictor_ResponseSyntax) **   <a name="forecast-DescribePredictor-response-TrainingParameters"></a>
The default training parameters or overrides selected during model training\. If using the AutoML algorithm or if HPO is turned on while using the DeepAR\+ algorithms, the optimized values for the chosen hyperparameters are returned\. For more information, see [Choosing an Amazon Forecast Algorithm](aws-forecast-choosing-recipes.md)\.  
Type: String to string map  
Key Length Constraints: Maximum length of 256\.  
Key Pattern: `^[a-zA-Z0-9\-\_\.\/\[\]\,\\]+$`   
Value Length Constraints: Maximum length of 256\.  
Value Pattern: `^[a-zA-Z0-9\-\_\.\/\[\]\,\"\\\s]+$` 

## Errors<a name="API_DescribePredictor_Errors"></a>

 **InvalidInputException**   
We can't process the request because it includes an invalid value or a value that exceeds the valid range\.  
HTTP Status Code: 400

 **ResourceNotFoundException**   
We can't find a resource with that Amazon Resource Name \(ARN\)\. Check the ARN and try again\.  
HTTP Status Code: 400

## See Also<a name="API_DescribePredictor_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/forecast-2018-06-26/DescribePredictor) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/forecast-2018-06-26/DescribePredictor) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/forecast-2018-06-26/DescribePredictor) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/forecast-2018-06-26/DescribePredictor) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/forecast-2018-06-26/DescribePredictor) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/forecast-2018-06-26/DescribePredictor) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/forecast-2018-06-26/DescribePredictor) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/forecast-2018-06-26/DescribePredictor) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/forecast-2018-06-26/DescribePredictor) 