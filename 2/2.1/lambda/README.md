# AWS Lambda

## Concepts

> AWS Lambda is a compute service that lets you run code without provisioning or managing servers. AWS Lambda executes your code only when needed and scales automatically, from a few requests per day to thousands per second. You pay only for the compute time you consume - there is no charge when your code is not running.

-AWS-[What is AWS Lambda?](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)

> AWS Lambda supports multiple languages through the use of runtimes.

&nbsp;

> When your function is invoked, Lambda attempts to re-use the execution environment from a previous invocation if one is available. This saves time preparing the execution environment, and allows you to save resources like database connections and temporary files in the execution context to avoid creating them every time your function runs.

-AWS-[AWS Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html)

> Function: A function is a resource that you can invoke to run your code in AWS Lambda. 

&nbsp;

> Qualifier: When you invoke or view a function, you can include a qualifier to specify a version or alias. A version is an immutable snapshot of a function's code and configuration that has a numerical qualifier.

&nbsp;

> Runtime: Lambda runtimes allow functions in different languages to run in the same base execution environment. You configure your function to use a runtime that matches your programming language.

&nbsp;

> Event: An event is a JSON formatted document that contains data for a function to process.

&nbsp;

> Concurrency: Concurrency is the number of requests that your function is serving at any given time.

&nbsp;

> Trigger: A trigger is a resource or configuration that invokes a Lambda function.

-AWS-[AWS Lambda concepts](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-concepts.html)

> AWS Lambda limits the amount of compute and storage resources that you can use to run and store functions. The following limits apply per-region and can be increased. 

* Concurrent executions: 1,000

* Function timeout: 900 seconds (15 minutes)

* Invocation frequency per Region (requests per second): 10 x Concurrent executions; unlimited for AWS triggers

* Deployment package size: 50 MB (zipped, for direct upload)

-AWS-[AWS Lambda limits](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-limits.html)

> An AWS Lambda function's execution role grants it permission to access AWS services and resources. You provide this role when you create a function, and Lambda assumes the role when your function is invoked. You can create an execution role for development that has permission to send logs to Amazon CloudWatch and upload trace data to AWS X-Ray.

&nbsp;

> AWS Lambda supports resource-based permissions policies for Lambda functions and layers. Resource-based policies let you grant usage permission to other accounts on a per-resource basis. You also use a resource-based policy to allow an AWS service to invoke your function.

&nbsp;

> You can use identity-based policies in AWS Identity and Access Management (IAM) to grant users in your account access to Lambda.

&nbsp;

> Lambda provides managed policies that grant access to Lambda API actions and, in some cases, access to other services used to develop and manage Lambda resources.

* AWSLambdaFullAccess – Grants full access to AWS Lambda actions and other services used to develop and maintain Lambda resources.

* AWSLambdaReadOnlyAccess – Grants read-only access to AWS Lambda resources.

* AWSLambdaRole – Grants permissions to invoke Lambda functions.

-AWS-[AWS Lambda execution role](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html)

## Exercises

TODO
