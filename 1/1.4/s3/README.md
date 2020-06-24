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

> As a general rule, AWS recommends using S3 bucket policies or IAM policies for access control. S3 ACLs is a legacy access control mechanism that predates IAM. However, if you already use S3 ACLs and you find them sufficient, there is no need to change.

&nbsp;

> An S3 ACL is a sub-resource that’s attached to every S3 bucket and object. It defines which AWS accounts or groups are granted access and the type of access. When you create a bucket or an object, Amazon S3 creates a default ACL that grants the resource owner full control over the resource.

-AWS-[IAM Policies and Bucket Policies and ACLs! Oh, My! (Controlling Access to S3 Resources)](https://aws.amazon.com/blogs/security/iam-policies-and-bucket-policies-and-acls-oh-my-controlling-access-to-s3-resources/)

&nbsp;

> The Amazon S3 Block Public Access feature provides settings for access points, buckets, and accounts to help you manage public access to Amazon S3 resources. By default, new buckets, access points, and objects don't allow public access. However, users can modify bucket policies, access point policies, or object permissions to allow public access. S3 Block Public Access settings override these policies and permissions so that you can limit public access to these resources.

### Static Website

> To host a static website on Amazon S3, you configure an Amazon S3 bucket for website hosting and then upload your website content to the bucket. When you configure a bucket as a static website, you must enable website hosting, set permissions, and create and add an index document. Depending on your website requirements, you can also configure redirects, web traffic logging, and a custom error document.

-AWS-[Hosting a static website on Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html)

**note:** Only supports HTTP.

> Server access logging provides detailed records for the requests that are made to a bucket. Server access logs are useful for many applications. For example, access log information can be useful in security and access audits. It can also help you learn about your customer base and understand your Amazon S3 bill.

-AWS-[Amazon S3 server access logging](https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerLogs.html)

### Versioning

> Use Amazon S3 Versioning to keep multiple versions of an object in one bucket. For example, you could store my-image.jpg (version 111111) and my-image.jpg (version 222222) in a single bucket. S3 Versioning protects you from the consequences of unintended overwrites and deletions. You can also use it to archive objects so that you have access to previous versions.

&nbsp;

> You must explicitly enable S3 Versioning on your bucket. By default, S3 Versioning is disabled.

&nbsp;

> When you DELETE an object, all versions remain in the bucket and Amazon S3 inserts a delete marker, as shown in the following figure.

-AWS-[Object Versioning](https://docs.aws.amazon.com/AmazonS3/latest/dev/ObjectVersioning.html)

### S3 Batch Operations

> You can use S3 Batch Operations to perform large-scale batch operations on Amazon S3 objects. S3 Batch Operations can execute a single operation or action on lists of Amazon S3 objects that you specify.

&nbsp;

> To create a job, you give S3 Batch Operations a list of objects and specify the action to perform on those objects. S3 Batch Operations support the following operations:

* PUT copy object

* PUT object tagging

* PUT object ACL

* Initiate S3 Glacier restore

* Invoke an AWS Lambda function

> The objects that you want a job to act on are listed in a manifest object. A job performs the specified operation on each object that is included in its manifest. You can use a CSV-formatted Amazon S3 inventory report as a manifest, which makes it easy to create large lists of objects located in a bucket.

-AWS-[The basics: S3 Batch Operations](https://docs.aws.amazon.com/AmazonS3/latest/dev/batch-ops-basics.html)

> Amazon S3 must have your permissions to perform S3 Batch Operations on your behalf. You grant these permissions through an AWS Identity and Access Management (IAM) role.

-AWS-[Granting permissions for Amazon S3 Batch Operations](https://docs.aws.amazon.com/AmazonS3/latest/dev/batch-ops-iam-role-policies.html)

### Cross-Origin Resource Sharing (CORS)

> Cross-origin resource sharing (CORS) defines a way for client web applications that are loaded in one domain to interact with resources in a different domain. With CORS support, you can build rich client-side web applications with Amazon S3 and selectively allow cross-origin access to your Amazon S3 resources.

&nbsp;

> To configure your bucket to allow cross-origin requests, you create a CORS configuration, which is an XML document with rules that identify the origins that you will allow to access your bucket, the operations (HTTP methods) that will support for each origin, and other operation-specific information.

-AWS-[Cross-origin resource sharing (CORS)](https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html)

### Storage Classes

> S3 Standard—The default storage class. If you don't specify the storage class when you upload an object, Amazon S3 assigns the S3 Standard storage class.

&nbsp;

> Reduced Redundancy—The Reduced Redundancy Storage (RRS) storage class is designed for noncritical, reproducible data that can be stored with less redundancy than the S3 Standard storage class.

&nbsp;

> We recommend that you not use this storage class. The S3 Standard storage class is more cost effective.

&nbsp;

> The S3 Standard-IA and S3 One Zone-IA storage classes are designed for long-lived and infrequently accessed data. (IA stands for infrequent access.) S3 Standard-IA and S3 One Zone-IA objects are available for millisecond access (same as the S3 Standard storage class). Amazon S3 charges a retrieval fee for these objects, so they are most suitable for infrequently accessed data.

&nbsp;

The S3 Standard-IA and S3 One Zone-IA storage classes are suitable for objects larger than 128 KB that you plan to store for at least 30 days. If an object is less than 128 KB, Amazon S3 charges you for 128 KB. If you delete an object before the end of the 30-day minimum storage duration period, you are charged for 30 days.

&nbsp;

> The S3 Intelligent-Tiering storage class stores objects in two access tiers: one tier that is optimized for frequent access and another lower-cost tier that is optimized for infrequently accessed data. For a small monthly monitoring and automation fee per object, Amazon S3 monitors access patterns of the objects in the S3 Intelligent-Tiering storage class and moves objects that have not been accessed for 30 consecutive days to the infrequent access tier.

&nbsp;

> There are no retrieval fees when using the S3 Intelligent-Tiering storage class. If an object in the infrequent access tier is accessed, it is automatically moved back to the frequent access tier. No additional tiering fees apply when objects are moved between access tiers within the S3 Intelligent-Tiering storage class.

&nbsp;

> The S3 Glacier and S3 Glacier Deep Archive storage classes are designed for low-cost data archiving. These storage classes offer the same durability and resiliency as the S3 Standard storage class.

&nbsp;

> S3 Glacier—Use for archives where portions of the data might need to be retrieved in minutes. Data stored in the S3 Glacier storage class has a minimum storage duration period of 90 days and can be accessed in as little as 1-5 minutes using expedited retrieval. If you have deleted, overwritten, or transitioned to a different storage class an object before the 90-day minimum, you are charged for 90 days.

&nbsp;

> S3 Glacier Deep Archive—Use for archiving data that rarely needs to be accessed. Data stored in the S3 Glacier Deep Archive storage class has a minimum storage duration period of 180 days and a default retrieval time of 12 hours. If you have deleted, overwritten, or transitioned to a different storage class an object before the 180-day minimum, you are charged for 180 days.

&nbsp;

> However, the S3 Glacier and S3 Glacier Deep Archive objects are not available for real-time access. You must first restore the S3 Glacier and S3 Glacier Deep Archive objects before you can access them.

&nbsp;

> Durability: 99.999999999 (11 9s) except RRS 99.99 (4 9s)

&nbsp;

> Availablity: 99.99 (4 9s) except: IA and Intel. Tiering 99.9 (3 9s) IA 1-Zone (99.5)

-AWS-[Amazon S3 Storage Classes](https://docs.aws.amazon.com/AmazonS3/latest/dev/storage-class-intro.html)

> The following are the available retrieval options when restoring an archived object:

* Expedited (Glacier: minutes) 
* Standard (Glacier: hours) (Deep Archive: 1 day)
* Bulk (Glacier: day) (Deep Archive: 2 day)

-AWS-[Restoring Archived Objects](https://docs.aws.amazon.com/AmazonS3/latest/dev/restoring-objects.html)

### Encryption

> You have the following options for protecting data at rest in Amazon S3:

&nbsp;

> Server-Side Encryption – Request Amazon S3 to encrypt your object before saving it on disks in its data centers and then decrypt it when you download the objects.

&nbsp;

> Client-Side Encryption – Encrypt data client-side and upload the encrypted data to Amazon S3. In this case, you manage the encryption process, the encryption keys, and related tools.

-AWS-[Protecting data using encryption](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html)

> Server-side encryption is the encryption of data at its destination by the application or service that receives it. Amazon S3 encrypts your data at the object level as it writes it to disks in its data centers and decrypts it for you when you access it. As long as you authenticate your request and you have access permissions, there is no difference in the way you access encrypted or unencrypted objects.

&nbsp;

> When you use Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3), each object is encrypted with a unique key. As an additional safeguard, it encrypts the key itself with a master key that it regularly rotates.

&nbsp;

> Server-Side Encryption with Customer Master Keys (CMKs) Stored in AWS Key Management Service (SSE-KMS) is similar to SSE-S3, but with some additional benefits and charges for using this service. There are separate permissions for the use of a CMK that provides added protection against unauthorized access of your objects in Amazon S3. SSE-KMS also provides you with an audit trail that shows when your CMK was used and by whom.

&nbsp;

> With Server-Side Encryption with Customer-Provided Keys (SSE-C), you manage the encryption keys and Amazon S3 manages the encryption, as it writes to disks, and decryption, when you access your objects.

-AWS-[Protecting data using server-side encryption
](https://docs.aws.amazon.com/AmazonS3/latest/dev/serv-side-encryption.html)

> SSE-C: When you upload an object, Amazon S3 uses the encryption key you provide to apply AES-256 encryption to your data and removes the encryption key from memory. When you retrieve an object, you must provide the same encryption key as part of your request. Amazon S3 first verifies that the encryption key you provided matches and then decrypts the object before returning the object data to you.

-AWS-[Protecting data using server-side encryption with customer-provided encryption keys (SSE-C)](https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerSideEncryptionCustomerKeys.html)

### Transfer Acceleration

> Amazon S3 Transfer Acceleration enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket. Transfer Acceleration takes advantage of Amazon CloudFront’s globally distributed edge locations. As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path.

-AWS-[Amazon S3 Transfer Acceleration](https://docs.aws.amazon.com/AmazonS3/latest/dev/transfer-acceleration.html)

### Lifecycle Management

> To manage your objects so that they are stored cost effectively throughout their lifecycle, configure their Amazon S3 Lifecycle. An S3 Lifecycle configuration is a set of rules that define actions that Amazon S3 applies to a group of objects. There are two types of actions:

&nbsp;

> Transition actions—Define when objects transition to another storage class. For example, you might choose to transition objects to the S3 Standard-IA storage class 30 days after you created them, or archive objects to the S3 Glacier storage class one year after creating them.

&nbsp;

> Expiration actions—Define when objects expire. Amazon S3 deletes expired objects on your behalf.

-AWS-[Object lifecycle management](https://docs.aws.amazon.com/AmazonS3/latest/dev/object-lifecycle-mgmt.html)

### Replication

> Replication enables automatic, asynchronous copying of objects across Amazon S3 buckets. Buckets that are configured for object replication can be owned by the same AWS account or by different accounts. You can copy objects between different AWS Regions or within the same Region.

&nbsp;

> Both source and destination buckets must have versioning enabled.

&nbsp;

> Amazon S3 must have permissions to replicate objects from the source bucket to the destination bucket on your behalf.

&nbsp;

> If the source bucket has S3 Object Lock enabled, the destination bucket must also have S3 Object Lock enabled.

-AWS-[Replication](https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html)

> By default Amazon S3 doesn't replicate the following:

&nbsp;

> Objects that existed before you added the replication configuration to the bucket.

&nbsp;

> Objects created with server-side encryption using customer-provided (SSE-C) encryption keys.

&nbsp;

> Objects created with server-side encryption using CMKs stored in AWS KMS. By default, Amazon S3 does not replicate objects encrypted using KMS CMKs. However, you can explicitly enable replication of these objects in the replication configuration, and provide relevant information so that Amazon S3 can replicate these objects.

&nbsp;

> Objects that are stored in S3 Glacier or S3 Glacier Deep Archive storage class.

&nbsp;

> Objects in the source bucket that the bucket owner doesn't have permissions for (when the bucket owner is not the owner of the object).

&nbsp;

> Updates to bucket-level subresources. For example, if you change the lifecycle configuration or add a notification configuration to your source bucket, these changes are not applied to the destination bucket.

&nbsp;

> Actions performed by lifecycle configuration.

&nbsp;

> If using the latest version of the replication configuration (the XML specifies Filter as the child of Rule), delete markers created either by a user action or by Amazon S3 as part of the lifecycle action are not replicated.

&nbsp;

> Objects in the source bucket that are replicas that were created by another replication rule.

&nbsp;

> To enable existing object replication for your account, you must contact AWS Support.

-AWS-[What Does Amazon S3 Replicate?](https://docs.aws.amazon.com/AmazonS3/latest/dev/replication-what-is-isnot-replicated.html)

### Object Locking

> With S3 Object Lock, you can store objects using a write-once-read-many (WORM) model. You can use it to prevent an object from being deleted or overwritten for a fixed amount of time or indefinitely. Object Lock helps you meet regulatory requirements that require WORM storage, or simply add another layer of protection against object changes and deletion.

-AWS-[Locking objects using S3 Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/dev/object-lock.html)

### Access Points

> Amazon S3 Access Points simplify managing data access at scale for shared datasets in S3. Access points are named network endpoints that are attached to buckets that you can use to perform S3 object operations, such as GetObject and PutObject. Each access point has distinct permissions and network controls that S3 applies for any request that is made through that access point. Each access point enforces a customized access point policy that works in conjunction with the bucket policy that is attached to the underlying bucket. You can configure any access point to accept requests only from a virtual private cloud (VPC) to restrict Amazon S3 data access to a private network. You can also configure custom block public access settings for each access point.

-AWS-[Managing data access with Amazon S3 access points](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-points.html)

## Exercises

### Create a Bucket

1. Create a Bucket in a Region with (mostly) globally unique name, e.g., *my-bucket-todosrus*

2. Observe bucket ownership

### Create an Object

1. Create an object in Bucket, e.g., image

2. Observe object ownership

### Make Bucket Objects Public

#### Assumptions

Assume reader understands IAM

#### Tasks

1. Confirm that Bucket Objects are not public

2. Try to use Bucket Policy to make Object public (see below); it fails

3. Disable public block access

4. Try to use Bucket Policy again

5. Observe that can access Bucket Object (incognito window)

Bucket Policy

```json
 {
  "Version":"2012-10-17",
  "Statement":[
    {
      "Effect":"Allow",
      "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::a-example/*"]
    }
  ]
}
```

### Make Bucket Static Website

1. Enable static website hosting on bucket

2. Create *index.html* file using image

3. View in browser

### Enable Bucket Server Access Logging

1. Enable bucket server access logging

**note**: It can take up to an hour to take effect.

### Set Content-Type Meta-Data on All Objects

1. Set Content-Type meta-data on all Objects

### Version an Object

1. Enable Bucket versioning

2. Upload new version of cat.jpg

3. Observe multiple versions

4. Delete Object

5. Restore Object (delete the delete marker)

### Create S3 Batch Operations Job

1. Create S3 Batch Operation to update a Tag

#### Supplemental Tasks

1. Clean up a bunch of stuff
