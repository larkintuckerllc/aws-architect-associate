# 2.4 Choose high-performing database solutions for a workload

* [Amazon Aurora](aurora)

* [Amazon DynamoDB](dynamodb)

* [Amazon ElastiCache](elasticache)

* [Amazon Relational Database Service (RDS)](rds)

* Amazon DocumentDB: Amazon DocumentDB (with MongoDB compatibility) is a fast, reliable, and fully managed database service. Amazon DocumentDB makes it easy to set up, operate, and scale MongoDB-compatible databases in the cloud. With Amazon DocumentDB, you can run the same application code and use the same drivers and tools that you use with MongoDB.

* Amazon Redshift: Amazon Redshift is an enterprise-level, petabyte scale, fully managed data warehousing service.

**note:** A Cloud Guru: 1 AZ, backup 1 day (default) to 35, maintains 3 copies (one in S3), can replicate snapshot in S3 in another region

* AWS Database Migration Service (AWS DMS) is a cloud service that makes it easy to migrate relational databases, data warehouses, NoSQL databases, and other types of data stores. You can use AWS DMS to migrate your data into the AWS Cloud, between on-premises instances (through an AWS Cloud setup), or between combinations of cloud and on-premises setups.

With AWS DMS, you can perform one-time migrations, and you can replicate ongoing changes to keep sources and targets in sync. If you want to change database engines, you can use the AWS Schema Conversion Tool (AWS SCT) to translate your database schema to the new platform. You then use AWS DMS to migrate the data. Because AWS DMS is a part of the AWS Cloud, you get the cost efficiency, speed to market, security, and flexibility that AWS services offer.
