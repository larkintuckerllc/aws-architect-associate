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

> When you invoke a function, you can choose to invoke it synchronously or asynchronously. With synchronous invocation, you wait for the function to process the event and return a response. With asynchronous invocation, Lambda queues the event for processing and returns a response immediately. For asynchronous invocation, Lambda handles retries and can send invocation records to a destination.

-AWS-[Invoking AWS Lambda functions](https://docs.aws.amazon.com/lambda/latest/dg/lambda-invocation.html)

### Specifics

> You can use environment variables to store secrets securely and adjust your function's behavior without updating code. An environment variable is a pair of strings that are stored in a function's version-specific configuration.

-AWS-[Using AWS Lambda environment variables](https://docs.aws.amazon.com/lambda/latest/dg/configuration-envvars.html)

> The system creates a new version of your Lambda function each time that you publish the function.

-AWS-[AWS Lambda function versions](https://docs.aws.amazon.com/lambda/latest/dg/configuration-versions.html)

> You can create one or more aliases for your AWS Lambda function. A Lambda alias is like a pointer to a specific Lambda function version.

-AWS-[AWS Lambda function aliases](https://docs.aws.amazon.com/lambda/latest/dg/configuration-aliases.html)

> You can configure your Lambda function to pull in additional code and content in the form of layers. A layer is a ZIP archive that contains libraries, a custom runtime, or other dependencies.

&nbsp;

> A function can use up to 5 layers at a time. The total unzipped size of the function and all layers can't exceed the unzipped deployment package size limit of 250 MB.

&nbsp;

> Your function can access the content of the layer during execution in the /opt directory. Layers are applied in the order that's specified, merging any folders with the same name. If the same file appears in multiple layers, the version in the last applied layer is used.

-AWS-[AWS Lambda layers](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html)

> You can configure a function to connect to private subnets in a virtual private cloud (VPC) in your account. Use Amazon Virtual Private Cloud (Amazon VPC) to create a private network for resources such as databases, cache instances, or internal services. Connect your function to the VPC to access private resources during execution.

-AWS-[Configuring a Lambda function to access resources in a VPC](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html)

> You can use the Lambda console to create an Amazon RDS Proxy database proxy for your function. A database proxy manages a pool of database connections and relays queries from a function. This enables a function to reach high concurrency levels without exhausting database connections.

-AWS-[Configuring database access for a Lambda function](https://docs.aws.amazon.com/lambda/latest/dg/configuration-database.html)

You can configure a function to mount an Amazon Elastic File System (Amazon EFS) file system to a local directory. With Amazon EFS, your function code can access and modify shared resources safely and at high concurrency.

-AWS-[Configuring file system access for Lambda functions](https://docs.aws.amazon.com/lambda/latest/dg/configuration-filesystem.html)

> An event source mapping is an AWS Lambda resource that reads from an event source and invokes a Lambda function. You can use event source mappings to process items from a stream or queue in services that don't invoke Lambda functions directly. Lambda provides event source mappings for the following services.

* Amazon Kinesis

* Amazon DynamoDB

* Amazon Simple Queue Service

> An event source mapping uses permissions in the function's execution role to read and manage items in the event source.

-AWS-[AWS Lambda event source mappings](https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventsourcemapping.html)

## Exercises

### Create a Function

1. Create function; Author from Scratch; Name: hello-lambda

2. Observe Role, Policy

3. Observe qualifiers ($LATEST and unqualified)

4. Execute a Test; Observe Log Group (for Function) in CloudWatch Logs (and Log Stream)

### Use Environment Variable

1. Create environment variable; HELLO: world

2. Update code to use environment variable

3. Run Test

### Publish a Version / Create Alias

1. Publish version of hello-lambda

2. Observe version (code and env. variable) is immutable; Make change to $LATEST

3. Create alias to version

### Create a Layer and Use

1. Create folder nodejs; npm init; install *random-words* npm library

2. zip folder

3. create S3 bucket with zip file

4. Run *aws* CLI to create layer

5. Attach Lambda to layer and use
