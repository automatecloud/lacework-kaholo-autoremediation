# AutoRemediation for the Lacework Policy LW_S3_9

## Description
Ensure the bucket ACL does not grant AWS users WRITE_ACP permission [modify bucket
ACL]

The S3 bucket ACL gives any authenticated AWS user permission to write [or re-write] the bucket
ACL. It is best practice to restrict WRITE_ACL permission to only principals who require it.
Rationale:
Granting all AWS users WRITE_ACL permission allows all AWS users to write [or re-write] the
bucket ACL. Malicious users can create temporary AWS accounts and use this permission to
change a hidden bucket to a public bucket by granting 'READ and ‘WRITE’ permission to
‘Everyone’ – see LW_S3_1 & LW_S3_1

### Severity
Critical

### Control ID
LW_S3_9

### Remediation Steps to manually fix this

Perform the following to revoke WRITE_ACL permission for all AWS users:
1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. From the list of buckets, select the bucket you want to change
4. Navigate to the permissions tab
5. Select 'Access Control List' from the 'Permissions' tab
6. Under Public access, Select the Group ‘Any AWS user’ by clicking the circular button in front
of it
7. Uncheck the ‘Write bucket permission’ under ‘Access to this bucket’s ACL’
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
