# Revert Changes Inbound rules to  Amazon VPC Security Groups Automatically and Receive Notifications.
The new ingress rule added to security group, a CloudWatch event that continually monitors changes to your security groups detects the new ingress rule and invokes Lambda function.Lambda function determines whether you are monitoring this security group . Reverts the new security group ingress rule. Sends you an SNS Notification email to let you know what the change was, who made it, and that the change was reverted.

If one of your staff members (inadvertently | mischievously) modifies your VPC security group to allow SSH access to the world, you want the change to be automatically reverted and then receive a notification that the change to the security group was automatically reverted.

Here is how the process works,

   * Someone adds a new ingress rule to your security group
   * A CloudWatch event that continually monitors changes to your security groups detects the new ingress rule and invokes Lambda function
   * Lambda function determines whether you are monitoring this security group
   * Reverts the new security group ingress rule.
   * Optionally: Sends you an SNS Notification email to let you know what the change was, who made it, and that the change was reverted

![image](https://user-images.githubusercontent.com/55474202/215387352-ad5d717c-2663-4ae0-9815-23aba6c706da.png)

Pre-Requisities

We will need the following pre-requisites to successfully complete this activity,

   * AWS CloudTrail must be enabled in the AWS Region where the solution is deployed
   * VPC with custom Security Group that we intend to monitor.
   * Note down the security group id, we will need it later to update the lambda function
   * IAM Role - i.e Lambda Service Role - with EC2FullAccess permissions
        You may use an Inline policy with more restrictive permissions

# Step 1 - Configure Lambda Function- SG-Sentry-Bot
# Step 2 - Configure Lambda Triggers

We are going to use Cloudwatch Events that will be triggered by CloudTrail API

   * Choose Create a new Rule
    * Fill the Rule Name & Rule Description
    * For Rule Type - Choose Event pattern
        * Below that, Choose EC2 Service
        * In the next field, Choose AWS API call via CloudTrail
    * Check the Operation box,
        * In below field, Type/Choose both AuthorizeSecurityGroupIngress & AuthorizeSecurityGroupEgress
    * Enable Trigger by Checking the box
    * Click on Add and Save the Lambda Function
    
 # Step 3 - Testing the solution

* Navigate to the EC2 console and choose Security Groups and Choose the security group that we are monitoring. Add a new Inbound rule, for example SSH on   port 22 from 0.0.0.0/0.

* Adding this rule creates an EC2 AuthorizeSecurityGroupIngress service event, which triggers the Lambda function.

* After a few moments, choose the refresh button ( The "refresh" icon ) to see that the new ingress rule that you just created has been removed by the solution.
Summary

* We have demonstrated how you can automatically revert changes to a VPC security group and have a notification sent about the VPC SG changes.
Customizations

* You can use many of the lamdba configurations to customize it suit your needs,

    * Create a SNS topic and subscribe to it
    * Security: Run your lambda inside your VPC for added security
        Use a custom IAM Policy with restrictive permissions
 
    
