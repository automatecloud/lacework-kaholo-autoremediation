# AutoRemediation for the Lacework Policy LW_S3_5

## Description
Ensure the bucket ACL does not grant ‘Everyone’ FULL_CONTROL [READ, WRITE,
READ_ACP, WRITE_ACP]

The S3 bucket ACL gives 'Everyone' total control of the bucket and the bucket ACL. It is best
practice to restrict FULL_CONTROL.
Rationale:
Granting ‘Everyone’ FULL_CONTROL gives anyone, including anonymous users from the Internet,
total control of the bucket. Malicious users can exploit this permission to read, delete or steal
your data and/or misuse the resources in your account.

### Severity
Critical

### Control ID
LW_S3_5

### Remediation Steps to manually fix this

Perform the following to revoke FULL_CONTROL for ‘Everyone’:
1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. From the list of S3 buckets, select S3 bucket you want to change
4. Navigate to the permissions tab
5. Select Access Control List from the permissions tab
6. Under Public access, Select the Group Everyone by clicking the circular button in front of it
7. Uncheck the ‘Read Objects’ and ‘List objects’ under ‘Access to the objects’ and ‘Read Bucket
Permissions’ and ‘Write bucket permissions’ under ‘Access to this bucket’s ACL’
8. Click ‘Save’ to remove the permissions for ‘Everyone’
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
