# AutoRemediation for the Lacework Policy LW_S3_7

## Description
Ensure the bucket ACL does not grant AWS users WRITE permission [create, overwrite,
and delete S3 objects]

The S3 bucket ACL gives any authenticated AWS user permission to create, write and delete
objects in the bucket. It is best practice to restrict WRITE permission to only principals who
require it.
Rationale:
Granting all AWS users WRITE permission allows any authenticated AWS user to create, write and
delete bucket objects. Malicious users can create temporary AWS accounts and exploit this
permission to alter data, delete data and misuse your resources.

### Severity
Critical

### Control ID
LW_S3_7

### Remediation Steps to manually fix this

Perform the following to revoke WRITE permission for all AWS users:
1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. From the list of S3 buckets, select S3 bucket you want to change
4. Navigate to the permissions tab
5. Select Access Control List from the permissions tab
6. Under Public access, Select the Group ‘Any AWS user’ by clicking the circular button in front
of it
7. Uncheck ‘Write objects’ under ‘Access to the objects’
8. Click ‘Save’ to remove the permission for ‘Any AWS user’
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
