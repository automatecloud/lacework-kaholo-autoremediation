# AutoRemediation for the Lacework Policy LW_S3_16

## Description
Ensure the S3 bucket has versioning enabled

Versioning enables users to keep multiple versions of an object in a bucket. It is a good practice to
enable versioning.
Rationale:
Bucket versioning will allow users to recover objects, which were deleted or changed maliciously
or by mistake. For buckets with critical information, versioning can help thwart ransomware
attacks

### Severity
High

### Control ID
LW_S3_16

### Remediation Steps to manually fix this

Perform the following to enable Server access logging:
1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. Select S3 bucket you want to change
4. Navigate to the ‘Properties’ panel
5. Select the ‘Versioning’ box
6. Check ‘Enable versioning’ [you may have to change any lifecycle rules that you have created
to apply any object that becomes a previous version]
7. Click ‘Save’ to enable versioning

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
