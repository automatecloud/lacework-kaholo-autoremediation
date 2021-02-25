# AutoRemediation for the Lacework Policy LW_S3_11

## Description
Ensure the attached S3 bucket policy does not grant 'Allow' permission to everyone

The S3 Bucket policy gives 'Allow' permission to everyone. It is best practice to restrict policies to
specific principals for whom the permissions are intended.
Rationale:
Bucket policies can be very complex. By restricting principals, unintended policy permissions will
be limited to the target audience.

### Severity
Critical

### Control ID
LW_S3_11

### Remediation Steps to manually fix this

Perform the following to remove permissions for everyone from the S3 bucket:
1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. From the list of S3 buckets, select S3 bucket you want to change
4. Navigate to the permissions tab
5. Click on ‘Bucket Policy’ to view and edit the policy
6. In the policy, check any statement that has the Effect value set to "Allow" with a Principal
element set to "*" or "AWS":"*" and no conditions
7. To entirely disable entirely access to the API, remove the statement
8. To limit access to a specific AWS account or AWS IAM user, replace the unrestricted Principal
element with the Amazon Resource Name (ARN) of the AWS account or user
9. Click ‘Save’ to remove the unrestricted permissions
10. Repeat steps 3-9 for every bucket for which you want to change permissions

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
