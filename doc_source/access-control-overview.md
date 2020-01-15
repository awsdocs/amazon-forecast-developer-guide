# Overview of Managing Access Permissions to Your Amazon Forecast Resources<a name="access-control-overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access a resource are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\)\. Some services \(such as AWS Lambda\) also support attaching permissions policies to resources\. 

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When granting permissions, you decide who is getting the permissions, the resources they get permissions for, and the specific actions that you want to allow on those resources\.

**Topics**
+ [Amazon Forecast Resources and Operations](#access-control-resources)
+ [Understanding Resource Ownership](#access-control-resource-ownership)
+ [Managing Access to Resources](#manage-access-overview)
+ [Specifying Policy Elements: Resources, Actions, Effects, and Principals](#specify-policy-elements)
+ [Specifying Conditions in a Policy](#specifying-conditions-overview)

## Amazon Forecast Resources and Operations<a name="access-control-resources"></a>

Amazon Forecast, supports the following resources\. 


****  

| Resource Type | ARN Format | 
| --- | --- | 
| Dataset |  `arn:aws:forecast::region:account-id:ds/dataset-name`  | 
| Dataset group | arn:aws:forecast::region:account\-id:dsgroup/dataset\-group\-name | 
| Predictor | arn:aws:forecast::region:account\-id:predictor/predictor\-name | 

Amazon Forecast provides a set of operations to work with Amazon Forecast resources\. For a list of available operations, see the Amazon Forecast [Actions](API_Operations.md)\.

## Understanding Resource Ownership<a name="access-control-resource-ownership"></a>

The AWS account owns the resources that are created in the account, regardless of who created the resources\. Specifically, the resource owner is the AWS account of the [principal entity](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html) \(that is, the root account, an IAM user, or an IAM role\) that authenticates the resource creation request\. The following examples illustrate how this works:
+ If you use the root account credentials of your AWS account to create a dataset group, your AWS account is the owner of the resource\.
+ If you create an IAM user in your AWS account and grant permissions to create a dataset group to that user, the user can create a dataset group\. However, your AWS account, to which the user belongs, owns the dataset group resource\.
+ If you create an IAM role in your AWS account with permissions to create a dataset group, anyone who can assume the role can create a dataset group\. Your AWS account, to which the user belongs, owns the dataset group resource\. 

## Managing Access to Resources<a name="manage-access-overview"></a>

A *permissions policy* describes who has access to what\. The following section explains the options for creating permissions policies\.

**Note**  
This section discusses using IAM in the context of Amazon Forecast\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What Is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Permissions policies attached to an IAM identity are referred to as *identity\-based* policies \(IAM policies\)\. Permissions policies attached to a resource are referred to as *resource\-based* policies\. Amazon Forecast supports only identity\-based permissions policies\. 

**Topics**
+ [Identity\-Based Policies \(IAM Policies\)](#manage-access-iam-policies)
+ [Resource\-based Policies](#manage-access-resource-policies)

### Identity\-Based Policies \(IAM Policies\)<a name="manage-access-iam-policies"></a>

You can attach permissions policies to IAM identities\. For example, you can do the following:
+ **Attach a permissions policy to a user or a group in your account** – To grant a user permissions to create an Amazon Forecast resource, such as a dataset group, you can attach a permissions policy to a user or to a group that the user belongs to\.
+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – You can attach an identity\-based permissions policy to an IAM role to grant cross\-account permissions\. For example, the administrator in account A can create a role to grant cross\-account permissions to another AWS account \(for example, account B\) or an AWS service as follows:

  1. Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions on resources in account A\.

  1. Account A administrator attaches a trust policy to the role identifying account B as the principal who can assume the role\. 

  1. Account B administrator can then share the role with users in account B\. Doing this allows users in account B to create or access resources in account A on behalf of account A\. The principal in the trust policy can also be an AWS service principal if you want to grant an AWS service permissions to assume the role\.

  For more information about using IAM to delegate permissions, see [Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\.

Some of the Amazon Forecast actions \(for example, `CreateDatasetImportJob`\) require the user to pass an IAM role to Amazon Forecast so that the service can assume that role and its permissions\. To pass a role \(and its permissions\) to an AWS service, a user must have permissions to pass the role to the service\. To allow a user to pass a role to an AWS service, you must grant permission for the `iam:PassRole` action\. For more information, see [Granting a User Permissions to Pass a Role to an AWS Service](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_passrole.html) in the * IAM User Guide*\.

The following is an example permissions policy\. You attach it to an IAM user\. 

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
            "Effect": "Allow",
            "Action": [
                "forecast:GetForecast",
            ],
            "Resource": "arn:aws:forecast:region:acct-id:predictor/predictor-name"
      }
   ]
}
```

For more information about using identity\-based policies with Amazon Forecast, see [Using Identity\-based Policies \(IAM Policies\) for Amazon Forecast](using-identity-based-policies.md)\. For more information about users, groups, roles, and permissions, see [Identities \(Users, Groups, and Roles\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### Resource\-based Policies<a name="manage-access-resource-policies"></a>

Other services, such as Amazon S3, also support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. Amazon Forecast doesn't support resource\-based policies\.

## Specifying Policy Elements: Resources, Actions, Effects, and Principals<a name="specify-policy-elements"></a>

For each Amazon Forecast resource, the service defines a set of API operations\. To grant permissions for these API operations, Amazon Forecast defines a set of actions that you can specify in a policy\. For example, for the Amazon Forecast dataset resource, the following actions are defined: `CreateDataset`, `DeleteDataset`, and `DescribeDataset`\. Some API operations can require permissions for more than one action in order to perform the API operation\. For more information about resources and API operations, see [Amazon Forecast Resources and Operations](#access-control-resources) and [Actions](API_Operations.md)\.

The following are the most basic policy elements:
+ **Resource** – You use an Amazon Resource Name \(ARN\) to identify the resource that the identity\-based policy applies to\. For more information, see [Amazon Forecast Resources and Operations](#access-control-resources)\.
+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, you can use `forecast:CreateDataset` to create a dataset\.
+ **Effect** – You specify the effect, either allow or deny, when the user requests the specific action\. If you don't explicitly grant access to \(allow\) a resource, access is implicitly denied\. You can also explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access\.
+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. Amazon Forecast doesn't support resource\-based policies\.

To learn more about IAM policy syntax and to read policy descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table showing all of the Amazon Forecast API operations and the resources that they apply to, see [Amazon Forecast API Permissions: Actions, Permissions, and Resources Reference](api-permissions-reference.md)\. 

## Specifying Conditions in a Policy<a name="specifying-conditions-overview"></a>

When you grant permissions, you can use the IAM policy language to specify the conditions under which a policy should take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\.

To express conditions, you use predefined condition keys\. There are no condition keys specific to Amazon Forecast\. However, there are AWS\-wide condition keys that you can use as appropriate\. For an example of AWS\-wide keys used in an Amazon Forecast permissions policy, see [Permissions Required to Use the Amazon Forecast Console](using-identity-based-policies.md#console-permissions)\. For a complete list of AWS\-wide keys, see [ Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\.