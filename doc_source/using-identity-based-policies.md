# Using Identity\-based Policies \(IAM Policies\) for Amazon Forecast<a name="using-identity-based-policies"></a>

This topic provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\) and, thereby, grant permissions to perform operations on Amazon Forecast resources\.

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available to manage access to your Amazon Forecast resources\. For more information, see [Overview of Managing Access Permissions to Your Amazon Forecast Resources](access-control-overview.md)\. 

**Topics**
+ [Permissions Required to Use the Amazon Forecast Console](#console-permissions)
+ [AWS Managed \(Predefined\) Policies for Amazon Forecast](#access-policy-aws-managed-policies)
+ [Customer Managed Policy Examples](#access-policy-customer-managed-examples)

The following is an example of a permissions policy:

```
{
   "Version": "2012-10-17",
   "Statement": [{
      "Sid": "stmt-1",
      "Effect": "Allow",
      "Action": [
         "forecast:CreateDataset" ],
      "Resource": "*"
      }
   ],
   "Statement": [{
      "Sid": "stmt-2",
      "Effect": "Allow",
      "Action": [
         "forecast:CreateDatasetGroup" ],
      "Resource": "arn:aws:forecast:region:acct-id:ds/test*"
      }
   ],
}
```

The policy has two statements:
+ The first statement grants permission for the `forecast:CreateDataset` action\. The action grants a user permission to create any Amazon Forecast dataset\.
+ The second statement grants permission for the `forecast:CreateDatasetGroup` action\. The action restricts a user to only creating dataset groups that include Amazon Forecast datasets whose name starts with `test`\.

The policy doesn't specify the `Principal` element because you don't specify the principal who gets the permission in an identity\-based policy\. When you attach the policy to a user, the user is the implicit principal\. When you attach a permissions policy to an IAM role, the principal identified in the role's trust policy gets the permissions\. 

For a table showing all of the Amazon Forecast API operations and the resources that they apply to, see [Amazon Forecast API Permissions: Actions, Permissions, and Resources Reference](api-permissions-reference.md)\. 

## Permissions Required to Use the Amazon Forecast Console<a name="console-permissions"></a>

When you are using the console, you need to grant permissions to all of the Amazon Forecast APIs\. The permissions reference table lists the Amazon Forecast API operations and shows the required permissions for each operation\. For more information about Amazon Forecast API operations, see [Amazon Forecast API Permissions: Actions, Permissions, and Resources Reference](api-permissions-reference.md)\.   

## AWS Managed \(Predefined\) Policies for Amazon Forecast<a name="access-policy-aws-managed-policies"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. These AWS managed policies grant necessary permissions for common use cases so that you can avoid having to investigate which permissions are needed\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\. 

The following AWS managed policies, which you can attach to users in your account, are specific to Amazon Forecast:
+ **AmazonForecastMakerReadOnly** – Grants read\-only access to Amazon Forecast resources\. 
+ **AmazonForecastMakerFullAccess** – Grants full access to Amazon Forecast resources and all of the supported operations\.

You can review these permissions policies by signing in to the IAM console and searching for them\.

You can also create your own custom IAM policies to allow permissions for Amazon Forecast actions and resources\. You can attach these custom policies to the IAM users or groups that require them\. 

## Customer Managed Policy Examples<a name="access-policy-customer-managed-examples"></a>

In this section, you can find example user policies that grant permissions for various Amazon Forecast actions\. These policies work when you are using the AWS SDKs or the AWS CLI\. When you are using the console, see [Permissions Required to Use the Amazon Forecast Console](#console-permissions)\.

**Topics**
+ [Example 1: Grant Account Administrator Permissions](#example-managed-policy-full-admin)
+ [Example 2: Allow All Amazon Forecast Actions](#example-managed-policy-all-actions)

### Example 1: Grant Account Administrator Permissions<a name="example-managed-policy-full-admin"></a>

After you set up an account \(see [Sign Up for AWS](aws-forecast-set-up-aws-account.md)\), you create an administrator user to manage your account\. The administrator user can create users and manage their permissions\. 

To grant the administrator user all of the permissions available for your account, attach the following permissions policy to that user:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}
```

### Example 2: Allow All Amazon Forecast Actions<a name="example-managed-policy-all-actions"></a>

You might choose to create a user who has permissions for all Amazon Forecast actions but not for any of your other services \(think of this user as a service\-specific administrator\)\. Attach the following permissions policy to this user: 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "forecast:*"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "kms:GenerateDataKey",
                "kms:Encrypt",
                "kms:Decrypt",
                "kms:DescribeKey",
                "kms:CreateGrant",
                "kms:RetireGrant",
                "kms:ListGrants"
            ],
            "Resource": [
                "arn:aws:s3:::*Forecast*",
                "arn:aws:s3:::*forecast*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:PutObject",
                "s3:DeleteObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::*Forecast*",
                "arn:aws:s3:::*forecast*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:PassRole"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "iam:PassedToService": "forecast.amazonaws.com"
                }
            }
        }
    ]
}
```