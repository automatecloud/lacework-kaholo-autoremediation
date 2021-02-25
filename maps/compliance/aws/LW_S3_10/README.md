# AutoRemediation for the Lacework Policy LW_S3_10

## Description
Ensure the bucket ACL does not grant AWS users FULL_CONTROL [READ, WRITE,
READ_ACP, WRITE_ACP]

The S3 bucket ACL gives any authenticated AWS user total control of the bucket and the bucket
ACL. It is best practice to restrict FULL_CONTROL.
Rationale:
Granting all AWS users FULL_CONTROL gives any authenticated AWS user total control of the
bucket. Malicious users can create temporary accounts and exploit this permission to read, delete
or steal your data and/or misuse the resources in your account.

### Severity
Critical

### Control ID
LW_S3_9

### Remediation Steps to manually fix this

Perform the following to revoke FULL_ACCESS permission for all authenticated AWS users:
1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. From the list of S3 buckets, select S3 bucket you want to change
4. Navigate to the permissions tab
5. Select Access Control List from the permissions tab
6. Under Public access, Select the Group ‘Any AWS user’ by clicking the circular button in front
of it
7. Uncheck the ‘Read Objects’ and ‘List objects’ under ‘Access to the objects’ and ‘Read Bucket
Permissions’ and ‘Write bucket permissions’ under ‘Access to this bucket’s ACL’
8. Click "Save" to remove the permissions for all AWS users
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
