# AutoRemediation for the Lacework Policy AWS_CIS_1_6

## Description
Ensure IAM password policy require at least one lowercase letter
(Scored)

Password policies are, in part, used to enforce password complexity requirements. IAM
password policies can be used to ensure password are comprised of different character
sets. It is recommended that the password policy require at least one lowercase letter.

**Rationale:**
Setting a password complexity policy increases account resiliency against brute force login
attempts.

### Severity
Medium

### Control ID
AWS_CIS_1_6

### Remediation Steps to manually fix this

Via the AWS Console
1. Login to AWS Console (with appropriate permissions to View Identity Access
Management Account Settings)
2. Go to IAM Service on the AWS Console
22 | P a g e
3. Click on Account Settings on the Left Pane
4. Check "Requires at least one lowercase letter"
5. Click "Apply password policy"
Via CLI
```
aws iam update-account-password-policy --require-lowercase-characters
```
**Note:** All commands starting with "aws iam update-account-password-policy" can be
combined into a single command.
