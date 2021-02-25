# AutoRemediation for the Lacework Policy LW_S3_3

## Description
Ensure the bucket ACL does not grant ‘Everyone’ READ_ACP permission [read bucket ACL]

The S3 bucket ACL gives 'Everyone' permission to read the bucket ACL. It is best practice to
restrict READ_ACL permission to only principals who require it.
Rationale:
Granting ‘Everyone’ READ_ACL permission allows anyone, including anonymous users from the
Internet, to read the bucket ACL. Malicious users can use this information to identify and exploit
objects with misconfigured permissions.

### Severity
Critical

### Control ID
LW_S3_3

### Remediation Steps to manually fix this

Perform the following to revoke READ_ACL permission for 'Everyone':
1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. From the list of buckets, select the bucket you want to change
4. Navigate to the permissions tab
5. Select Access Control List from the permissions tab
6. Under Public access, Select the Group ‘Everyone’ by clicking the circular button in front of it
7. Uncheck the ‘Read bucket permissions’ under ‘Access to this bucket’s ACL’
8. Click ‘Save’ to remove the permission for ‘Everyone’
9. Repeat steps 3-8 for every bucket for which you want to change permissions

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
