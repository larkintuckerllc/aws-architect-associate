# Amazon S3 Glacier

## Concepts

Amazon S3 Glacier is a secure, durable, and extremely low-cost Amazon S3 storage class for data archiving and long-term backup.

In S3 Glacier, a vault is a Glacier Glacier storing archives. When you create a vault, you specify a name and choose an AWS Region where you want to create the vault.

An archive can be any data such as a photo, video, or document and is a base unit of storage in S3 Glacier. Each archive has a unique ID and an optional description. Note that you can only specify the optional description during the upload of an archive. S3 Glacier assigns the archive an ID, which is unique in the AWS Region in which it is stored.

Any archive operation, such as upload, download, or deletion, requires that you use the AWS Command Line Interface (CLI) or write code. There is no console support for archive operations.

When you make a request to retrieve data from S3 Glacier, you initiate a retrieval job for an archive. Once the retrieval job completes, your data will be available to download or access it using Amazon Elastic Compute Cloud (Amazon EC2) for 24 hours. 

Yes, all data in the service will be encrypted on the server side. Amazon S3 Glacier handles key management and key protection for you. Amazon S3 Glacier uses one of the strongest block ciphers available, 256-bit Advanced Encryption Standard (AES-256). 256-bit is the largest key size defined for AES. Customers wishing to manage their own keys can encrypt data prior to uploading it.

Vault Lock allows you to easily deploy and enforce compliance controls on individual S3 Glacier vaults via a lockable policy (Vault Lock policy). Once locked, the Vault Lock policy becomes immutable and S3 Glacier will enforce the prescribed controls to help achieve your compliance objectives.
