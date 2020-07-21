# Amazon Simple Notification Service (SNS)

## Concepts

> Amazon Simple Notification Service (Amazon SNS) is a web service that coordinates and manages the delivery or sending of messages to subscribing endpoints or clients. In Amazon SNS, there are two types of clients—publishers and subscribers—also referred to as producers and consumers. Publishers communicate asynchronously with subscribers by producing and sending a message to a topic, which is a logical access point and communication channel. Subscribers (that is, web servers, email addresses, Amazon SQS queues, AWS Lambda functions) consume or receive the message or notification over one of the supported protocols (that is, Amazon SQS, HTTP/S, email, SMS, Lambda) when they are subscribed to the topic.

-AWS-[What is Amazon SNS?](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)

> The "fanout" scenario is when an Amazon SNS message is sent to a topic and then replicated and pushed to multiple Amazon SQS queues, HTTP endpoints, or email addresses. This allows for parallel asynchronous processing.

&nbsp;

> Application and system alerts are notifications that are triggered by predefined thresholds and sent to specified users by SMS and/or email.

&nbsp;

> Application and system alerts are notifications that are triggered by predefined thresholds and sent to specified users by SMS and/or email.

&nbsp;

> Mobile push notifications enable you to send messages directly to mobile apps.

&nbsp;

> Amazon SNS provides durable storage of all messages that it receives. When Amazon SNS receives your Publish request, it stores multiple copies of your message to disk. Before Amazon SNS confirms to you that it received your request, it stores the message in multiple isolated locations known as Availability Zones. The message is stored in Availability Zones that are located within your chosen AWS Region, such as the US East (N. Virginia) Region.

-AWS-[Common Amazon SNS scenarios](https://docs.aws.amazon.com/sns/latest/dg/sns-common-scenarios.html)

> After you configure the message delivery status attributes, log entries will be sent to CloudWatch Logs for messages sent to a topic subscribed to an Amazon SNS endpoint.

-AWS-[Amazon SNS message delivery status](https://docs.aws.amazon.com/sns/latest/dg/sns-topic-attributes.html)

> Amazon SNS defines a delivery policy for each delivery protocol. The delivery policy defines how Amazon SNS retries the delivery of messages when server-side errors occur (when the system that hosts the subscribed endpoint becomes unavailable). When the delivery policy is exhausted, Amazon SNS stops retrying the delivery and discards the message—unless a dead-letter queue is attached to the subscription.

-AWS-[Message delivery retries](https://docs.aws.amazon.com/sns/latest/dg/sns-message-delivery-retries.html)

> Amazon SNS supports delivery of message attributes, which let you provide structured metadata items (such as timestamps, geospatial data, signatures, and identifiers) about the message. Each message can have up to 10 attributes.

-AWS-[Amazon SNS message attributes](https://docs.aws.amazon.com/sns/latest/dg/sns-message-attributes.html)

> By default, an Amazon SNS topic subscriber receives every message published to the topic. To receive a subset of the messages, a subscriber must assign a filter policy to the topic subscription.

-AWS-[Amazon SNS message filtering](https://docs.aws.amazon.com/sns/latest/dg/sns-message-filtering.html)

## Exercises
