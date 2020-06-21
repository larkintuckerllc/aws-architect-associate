# Amazon Simple Storage System (S3)

## Concepts

### Overview

> Amazon Simple Storage Service is storage for the Internet. It is designed to make web-scale computing easier for developers.

-AWS-[What is Amazon S3?](https://docs.aws.amazon.com/AmazonS3/latest/dev/Welcome.html)

> A bucket is a container for objects stored in Amazon S3. Every object is contained in a bucket.

&nbsp;

> You can configure buckets so that they are created in a specific AWS Region.

&nbsp;

> Objects are the fundamental entities stored in Amazon S3. Objects consist of object data and metadata. The data portion is opaque to Amazon S3. The metadata is a set of name-value pairs that describe the object. These include some default metadata, such as the date last modified, and standard HTTP metadata, such as Content-Type. You can also specify custom metadata at the time the object is stored.

&nbsp;

> A key is the unique identifier for an object within a bucket. Every object in a bucket has exactly one key. The combination of a bucket, key, and version ID uniquely identify each object. So you can think of Amazon S3 as a basic data map between "bucket + key + version" and the object itself. Every object in Amazon S3 can be uniquely addressed through the combination of the web service endpoint, bucket name, key, and optionally, a version

&nbsp;

> Amazon S3 provides read-after-write consistency for PUTS of new objects in your S3 bucket in all Regions with one caveat.

&nbsp;

> Amazon S3 offers eventual consistency for overwrite PUTS and DELETES in all Regions.

-AWS-[Introduction to Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/Introduction.html)

> A bucket is owned by the AWS account that created it. Bucket ownership is not transferable.

&nbsp;

> When you create a bucket, you choose its name and the Region to create it in. After you create a bucket, you can't change its name or Region.

&nbsp;

> By default, you can create up to 100 buckets in each of your AWS accounts. If you need additional buckets, you can increase your account bucket limit to a maximum of 1,000 buckets by submitting a service limit increase.

&nbsp;

> If a bucket is empty, you can delete it. After a bucket is deleted, the name becomes available for reuse. However, after you delete the bucket, you might not be able to reuse the name for various reasons. For example, when you delete the bucket and the name becomes available for reuse, another account might create a bucket with that name.

&nbsp;

> Bucket names must be unique within a partition. A partition is a grouping of Regions. AWS currently has three partitions: aws (Standard Regions), aws-cn (China Regions), and aws-us-gov (AWS GovCloud [US] Regions).

-AWS-[Bucket Restrictions and Limitations](https://docs.aws.amazon.com/AmazonS3/latest/dev/BucketRestrictions.html)

> Designed to provide 99.999999999% durability and 99.99% availability of objects over a given year

&nbsp;

> Designed to sustain the concurrent loss of data in two facilities

-AWS-[Data protection in Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/DataDurability.html)

### Permissions

> By default, all Amazon S3 resources—buckets, objects, and related subresources (for example, lifecycle configuration and website configuration)—are private: only the resource owner, an AWS account that created it, can access the resource. The resource owner can optionally grant access permissions to others by writing an access policy.

&nbsp;

> Amazon S3 offers access policy options broadly categorized as resource-based policies and user policies. Access policies you attach to your resources (buckets and objects) are referred to as resource-based policies. For example, bucket policies and access control lists (ACLs) are resource-based policies. You can also attach access policies to users in your account. These are called user policies. You may choose to use resource-based policies, user policies, or some combination of these to manage permissions to your Amazon S3 resources

-AWS-[Identity and access management in Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/s3-access-control.html)

### Storage Classes

TODO

### Versioning

TODO

### Encryption

TODO

### Transfer Acceleration

TODO

### Access Points

TODO

## Exercises

### Create a Bucket

1. Create a Bucket in a Region with (mostly) globally unique name, e.g., *my-bucket-todosrus*

2. Observe bucket ownership

### Create an Object

1. Create an object in Bucket

2. Observe object ownership
