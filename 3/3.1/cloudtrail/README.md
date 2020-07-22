# AWS CloudTrail

## Concepts

> AWS CloudTrail is an AWS service that helps you enable governance, compliance, and operational and risk auditing of your AWS account. Actions taken by a user, role, or an AWS service are recorded as events in CloudTrail. Events include actions taken in the AWS Management Console, AWS Command Line Interface, and AWS SDKs and APIs.

&nbsp;

-AWS-[What Is AWS CloudTrail?](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)

> CloudTrail is enabled on your AWS account when you create it. When activity occurs in your AWS account, that activity is recorded in a CloudTrail event. You can easily view events in the CloudTrail console by going to Event history.

&nbsp;

> Event history allows you to view, search, and download the past 90 days of activity in your AWS account. In addition, you can create a CloudTrail trail to archive, analyze, and respond to changes in your AWS resources. A trail is a configuration that enables delivery of events to an Amazon S3 bucket that you specify. You can also deliver and analyze events in a trail with Amazon CloudWatch Logs and Amazon CloudWatch Events.

&nbsp;

> You can create two types of trails for an AWS account:

* A trail that applies to all regions

* A trail that applies to one region

> If you have created an organization in AWS Organizations, you can also create a trail that will log all events for all AWS accounts in that organization. This is referred to as an organization trail. Organization trails can apply to all AWS Regions or one Region.

&nbsp;

> By default, CloudTrail event log files are encrypted using Amazon S3 server-side encryption (SSE). You can also choose to encrypt your log files with an AWS Key Management Service (AWS KMS) key.

&nbsp;

> CloudTrail typically delivers log files within 15 minutes of account activity. In addition, CloudTrail publishes log files multiple times an hour, about every five minutes.

-AWS-[How CloudTrail Works](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/how-cloudtrail-works.html)

> Management events provide information about management operations that are performed on resources in your AWS account. These are also known as control plane operations.

&nbsp;

> Data events provide information about the resource operations performed on or in a resource. These are also known as data plane operations. Data events are often high-volume activities. The following two data types are recorded:

* Amazon S3 object-level API activity (for example, GetObject, DeleteObject, and PutObject API operations).

* AWS Lambda function execution activity (the Invoke API).

> Data events are disabled by default when you create a trail.

&nbsp;

> CloudTrail Insights events capture unusual activity in your AWS account. If you have Insights events enabled, and CloudTrail detects unusual activity, Insights events are logged to a different folder or prefix in the destination S3 bucket for your trail.

&nbsp;

> Insights events are disabled by default when you create a trail.

&nbsp;

> Integration with CloudWatch Logs enables CloudTrail to send events containing API activity in your AWS account to a CloudWatch Logs log group. CloudTrail events that are sent to CloudWatch Logs can trigger alarms according to the metric filters you define.

&nbsp;

> Sending data that is logged by CloudTrail to CloudWatch Logs or CloudWatch Events requires that you have at least one trail.

## Exercises

Follow:

[Getting Started with AWS CloudTrail Tutorial](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-tutorial.html)

[Monitoring CloudTrail Log Files with Amazon CloudWatch Logs](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/monitor-cloudtrail-log-files-with-cloudwatch-logs.html)

Cleanup:

Trail

Bucket