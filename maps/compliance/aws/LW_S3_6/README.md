# AutoRemediation for the Lacework Policy LW_S3_6

## Description
Ensure the bucket ACL does not grant AWS users READ permission [list S3 objects]

The S3 bucket ACL gives any authenticated AWS user permission to list objects, which allows any
authenticated AWS user to list the bucket contents. It is best practice to restrict READ permission
to only principals who require it.
Rationale:
Granting all AWS uses READ permission allows any authenticated AWS user to list all bucket
objects. Malicious users can create temporary AWS accounts and use this permission to identify
and exploit objects with misconfigured ACL permissions.

### Severity
Critical

### Control ID
LW_S3_6

### Remediation Steps to manually fix this

Perform the following to revoke READ permission for all AWS users:
1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. From the list of buckets, select the bucket you want to change
4. Navigate to the permissions tab
5. Select Access Control List from the permissions tab
6. Under Public access, uncheck the Group ‘Any AWS user’ by clicking the circular button in
front of it
7. Uncheck ‘List objects’ under ‘Access to the objects’
8. Click ‘Save to remove the permission for ‘Any AWS user’
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
