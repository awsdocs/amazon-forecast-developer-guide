# Retraining Predictors<a name="retrain-predictors"></a>

**Note**  
Retraining is only available for predictors created with AutoPredictor \([`CreateAutoPredictor`](API_CreateAutoPredictor.md)\)\. You can upgrade existing legacy predictors to AutoPredictor\. See [Upgrading to AutoPredictor](howitworks-predictor.md#upgrading-autopredictor)\.

Predictors can be retained with updated datasets to keep your predictors up to date\. When retraining a predictor, Amazon Forecast maintains the same predictor configuration settings\. After retraining, the original predictor will remain active and the retrained predictor will have a separate Predictor ARN\.

Retraining a predictor can improve forecasting accuracy in two ways:

1. **More current data**: Your retrained predictor will incorporate more up\-to\-date data when training a model\.

1. **Predictor improvements**: Your retrained predictor will incorporate any updates and improvements in the Amazon Forecast algorithms and additional datasets\.

Retraining a predictor can be up to 50% faster than creating a new predictor from scratch\. Predictor training times are faster and Forecast automatically uses your existing configuration settings\.

**Python notebooks**  
For a step\-by\-step guide on retraining predictors, see [Retraining a predictor](https://github.com/aws-samples/amazon-forecast-samples/blob/main/notebooks/advanced/Retraining_AutoPredictor/Retraining.ipynb)\.

You can retrain a predictor using the Software Development Kit \(SDK\) or the Amazon Forecast console\.

------
#### [ Console ]

**To retrain a predictor**

1. Sign in to the AWS Management Console and open the Amazon Forecast console at [https://console\.aws\.amazon\.com/forecast/](https://console.aws.amazon.com/forecast/)\.

1. In the navigation pane, choose **Predictors**\.

1. Choose the predictor to retrain\.

1. In the **Predictor actions** drop\-down, choose **Retrain**\.

1. Set a unique name for the upgraded predictor\.

1. Choose **Retrain predictor**\.

------
#### [ SDK ]

**To retrain a predictor**

Using the [`CreateAutoPredictor`](API_CreateAutoPredictor.md) operation, assign the predictor a unique name and set the value of `ReferencePredictorArn` to the predictor you wish to retrain\.

```
{
  "PredictorName": "RetrainedPredictor",
  "ReferencePredictorArn": "arn:aws:forecast:us-west-2:938097332257:predictor/OriginalPredictor"
}
```

When retraining a predictor, assign values to only the `PredictorName` and `ReferencePredictorArn` parameters\.

------