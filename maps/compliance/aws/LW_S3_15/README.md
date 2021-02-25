# AutoRemediation for the Lacework Policy LW_S3_15

## Description
Ensure all data is transported from the S3 bucket securely

Policies that require requests to use Secure Socket Layer (SSL) helps to secure data. It is good
practice to enable secure transport.
Rationale:
When S3 buckets are accessed without SSL, bucket data is not encrypted and open to man-inthe-middle attacks.

### Severity
High

### Control ID
LW_S3_15

### Remediation Steps to manually fix this

1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. Select S3 bucket you want to change
4. Navigate to the Permissions panel
5. Click on Bucket Policy to review and edit the policy
6. Ensure the following statement is present in the policy
{
"Sid": "DenyUnSecureCommunications",
"Effect": "Deny",
"Principal": "*",
"Action": "s3:*",
"Resource": "arn:aws:s3:::BUCKET-NAME",
"Condition": {
 "Bool": {
 "aws:SecureTransport": "false"
 }
}
}
7. Click ‘Save’ to enable secure transport
8. Repeat steps 3-6 for every bucket for which you want to change permissions

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
