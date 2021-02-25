# AutoRemediation for the Lacework Policy LW_S3_12

## Description
Ensure the S3 bucket requires MFA to delete objects

Objects in the bucket are able to be deleted according to bucket ACL or policy. If objects in the
bucket are considered ‘permanent’, MFA delete can help prevent accidental deletion by requiring
a second factor.
Rationale:
If objects are considered ‘permanent’, MFA helps prevent accidental deletion. Additionally, MFA
adds an extra level of security by preventing malicious users from intentionally deleting objects.

### Severity
Critical

### Control ID
LW_S3_12

### Remediation Steps to manually fix this

MFA delete must be enabled through the AWS CLI. Please see AWS documentation for a
complete understanding:
https://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html#MultiFactorAuthentication
Delete

<VersioningConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
 <Status>VersioningState</Status>
 <MfaDelete>MfaDeleteState</MfaDelete>
</VersioningConfiguration>

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
