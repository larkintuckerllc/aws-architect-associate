# Amazon CloudFront

## Concepts

> Amazon CloudFront is a web service that speeds up distribution of your static and dynamic web content, such as .html, .css, .js, and image files, to your users. CloudFront delivers your content through a worldwide network of data centers called edge locations. When a user requests content that you're serving with CloudFront, the user is routed to the edge location that provides the lowest latency (time delay), so that content is delivered with the best possible performance.

&nbsp;

> If the content is already in the edge location with the lowest latency, CloudFront delivers it immediately.

&nbsp;

> If the content is not in that edge location, CloudFront retrieves it from an origin that you've defined—such as an Amazon S3 bucket, a MediaPackage channel, or an HTTP server (for example, a web server) that you have identified as the source for the definitive version of your content.

-AWS-[What Is Amazon CloudFront?](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)

> You must allow public read access to the bucket and files so that CloudFront URLs can serve content from the bucket.

-AWS-[Getting Started with a Simple CloudFront Distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/GettingStarted.SimpleDistribution.html)

> Using Lambda@Edge with CloudFront enables a variety of ways to customize the content that CloudFront delivers.

-AWS-[CloudFront Use Cases](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/IntroductionUseCases.html)

**note:** A Cloud Guru; Cache Hit Ratio determines how effective caching is. To make effective;

* TTL: Use Cache-Control header on Origin

* Query parameters are case sensitive

* For cookies, can create cache behavior to ignore cookies (e.g., for static content)

* If enable caching based on request headers, be specific.

* If origin does not support compression, can disable checking Accept-Encoding header

### Signed URLs

> Many companies that distribute content over the internet want to restrict access to documents, business data, media streams, or content that is intended for selected users, for example, users who have paid a fee. To securely serve this private content by using CloudFront, you can do the following:

&nbsp;

> Require that your users access your private content by using special CloudFront signed URLs or signed cookies.

&nbsp;

> Require that your users access your content by using CloudFront URLs, not URLs that access content directly on the origin server (for example, Amazon S3 or a private HTTP server). Requiring CloudFront URLs isn't necessary, but we recommend it to prevent users from bypassing the restrictions that you specify in signed URLs or signed cookies.

-AWS-[Serving Private Content with Signed URLs and Signed Cookies](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/PrivateContent.html)

> S3: To require that users access your content through CloudFront URLs, you do the following tasks:

&nbsp;

> Create a special CloudFront user called an origin access identity and associate it with your CloudFront distribution.

-AWS-[Overview of Serving Private Content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-overview.html)

> IAM users can't create CloudFront key pairs. You must log in using root credentials to create key pairs.

&nbsp;

> Trusted signers are associated with cache behaviors. This allows you to require signed URLs or signed cookies for some files and not for others in the same distribution. Trusted signers can only create signed URLs or cookies for files that are associated with the corresponding cache behaviors

-AWS-[Specifying the AWS Accounts That Can Create Signed URLs and Signed Cookies (Trusted Signers)](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-trusted-signers.html)

### Misc

> If you need to remove a file from CloudFront edge caches before it expires, you can do one of the following:

* Invalidate the file from edge caches. The next time a viewer requests the file, CloudFront returns to the origin to fetch the latest version of the file.

* Use file versioning to serve a different version of the file that has a different name.

-AWS-[Invalidating Files](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Invalidation.html)

> AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to CloudFront, and lets you control access to your content. Based on conditions that you specify, such as the values of query strings or the IP addresses that requests originate from, CloudFront responds to requests either with the requested content or with an HTTP status code 403 (Forbidden). You can also configure CloudFront to return a custom error page when a request is blocked.

-AWS-[Using AWS WAF to Control Access to Your Content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-awswaf.html)

> You can use geo restriction, also known as geo blocking, to prevent users in specific geographic locations from accessing content that you're distributing through a CloudFront web distribution.

-AWS-[Restricting the Geographic Distribution of Your Content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/georestrictions.html)

> An HTTP 502 status code (Bad Gateway) indicates that CloudFront wasn't able to serve the requested object because it couldn't connect to the origin server.

&nbsp;

> An HTTP 503 status code (Service Unavailable) typically indicates a performance issue on the origin server. In rare cases, it indicates that CloudFront temporarily can’t satisfy a request because of resource constraints at an edge location.

&nbsp;

> CloudFront will return an HTTP 504 status code if traffic is blocked to the origin by a firewall or security group, or if the origin isn’t accessible on the internet.

-AWS-[Troubleshooting Error Responses from Your Origin](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/troubleshooting-response-errors.html)

## Exercises

### Create Basic Distribution

#### Assumptions

S3 Section

#### Tasks

1. Create S3 bucket with file *index.html*

2. Allow public access to bucket, make *index.html* public

3. Create Distribution
