# AutoRemediation for the Lacework Policy LW_S3_13

## Description
Ensure the S3 bucket has access logging enabled

Access logging provides records of requests that are made to a bucket. Access log information is
useful in security investigations and may be required for audit purposes. It is good practice review
bucket objects and enable server access logging as appropriate.
Rationale:
If the S3 bucket has access logging enabled, you will be able to track every request made to
access the bucket. Monitoring this activity can be used to detect anomalies and protect against
unauthorized access.

### Severity
Low

### Control ID
LW_S3_13

### Remediation Steps to manually fix this

Perform the following to enable server access logging:
1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. Select S3 bucket you want to change
4. Navigate to the ‘Properties’ panel
5. Select the ‘Server access logging’ box
6. Check ‘Enable logging’
7. Provide the name of the target bucket where the events will be logged
8. Provide the target prefix to provide a sub-directory within the bucket where the log will be
stored
9. Click ‘Save’ to enable logging
10. Repeat steps 3-9 for every bucket for which you want to audit s3 activity

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
