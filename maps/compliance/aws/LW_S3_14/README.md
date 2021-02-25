# AutoRemediation for the Lacework Policy LW_S3_14

## Description
Ensure all data stored in the S3 bucket is securely encrypted at rest

When server-side encryption is enabled, Amazon S3 encrypts data as it is written to disk and
decrypts it when accessed by users. It is good practice to enable S3 bucket encryption.
Rationale:
Encryption helps protect data from unauthorized users and attacks. Although client-side
encryption has advantages, it can be complex to implement. Server-side encryption adds a layer
of security if client encryption cannot be enabled.

### Severity
High

### Control ID
LW_S3_14

### Remediation Steps to manually fix this

AWS offers three encryption options:
• Use Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)
• Use Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS)
• Use Server-Side Encryption with Customer-Provided Keys (SSE-C)
Please refer to the AWS documentation to understand more and choose which is best for you:
https://docs.aws.amazon.com/AmazonS3/latest/dev/serv-side-encryption.html

## How can i use this Map?

**NEEDS TO BE DESCRIBED**

## Import the Map

**NEEDS TO BE DESCRIBED**

### Map Design and workflow

**NEEDS TO BE DESCRIBED**

### Map trigger

**NEEDS TO BE DESCRIBED**

### Configuration within the Map

**NEEDS TO BE DESCRIBED**

### Configuration of Slack Messages

**NEEDS TO BE DESCRIBED**

### Configuration of the Remediation block

**NEEDS TO BE DESCRIBED**

## Build an example curl webhook

T**NEEDS TO BE DESCRIBED**
