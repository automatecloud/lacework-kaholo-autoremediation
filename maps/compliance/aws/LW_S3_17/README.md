# AutoRemediation for the Lacework Policy LW_S3_17

## Description
Ensure that S3 bucket access is restricted to a whitelist of IP networks

S3 bucket access can be restricted to a whitelist of IP addresses. This allows the owners to have
greater control over network access to sensitive resources.
Rationale:
Whitelisting IP address access to S3 buckets can mitigate certain attacks and data theft. This
practice makes accessing the data in S3 more difficult for an attacker.

### Severity
High

### Control ID
LW_S3_17

### Remediation Steps to manually fix this

1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. Select S3 bucket you want to change
4. Navigate to the ‘Permissions’ panel
5. Select the ‘Bucket Policy’ box
6. Add a conditional statement that allows access from the IP addresses you define such as:
{
 "Version": "2012-10-17",
 "Id": "VPCe and SourceIP",
 "Statement": [{
 "Sid": "VPCe and SourceIP",
 "Effect": "Deny",
 "Principal": "*",
 "Action": "s3:*",
 "Resource": [
 "arn:aws:s3:::awsexamplebucket",
 "arn:aws:s3:::awsexamplebucket/*"
 ],
 "Condition": {
 "StringNotLike": {
 "aws:sourceVpce": [
 "vpce-1111111",
 "vpce-2222222"
 ]
 },
 "NotIpAddress": {
 "aws:SourceIp": [
 "11.11.11.11/32",
 "22.22.22.22/32"
 ]
 }
 }
 }]
}

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
