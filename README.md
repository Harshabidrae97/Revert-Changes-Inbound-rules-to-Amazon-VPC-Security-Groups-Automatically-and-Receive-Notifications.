# Revert Changes Inbound rules to  Amazon VPC Security Groups Automatically and Receive Notifications.
The new ingress rule added to security group, a CloudWatch event that continually monitors changes to your security groups detects the new ingress rule and invokes Lambda function.Lambda function determines whether you are monitoring this security group . Reverts the new security group ingress rule. Sends you an SNS Notification email to let you know what the change was, who made it, and that the change was reverted.

If one of your staff members (inadvertently | mischievously) modifies your VPC security group to allow SSH access to the world, you want the change to be automatically reverted and then receive a notification that the change to the security group was automatically reverted.

Here is how the process works,

    Someone adds a new ingress rule to your security group
    A CloudWatch event that continually monitors changes to your security groups detects the new ingress rule and invokes Lambda function
    Lambda function determines whether you are monitoring this security group
        Reverts the new security group ingress rule.
        Optionally: Sends you an SNS Notification email to let you know what the change was, who made it, and that the change was reverted
