# AutoRemediation for the Lacework Policy AWS_CIS_1_9

## Description
Ensure IAM password policy requires minimum length of 14 or
greater (Scored)

Password policies are, in part, used to enforce password complexity requirements. IAM
password policies can be used to ensure password are at least a given length. It is
recommended that the password policy require a minimum password length 14.

**Rationale:**
Setting a password complexity policy increases account resiliency against brute force login
attempts.

### Severity
Medium

### Control ID
AWS_CIS_1_9

### Remediation Steps to manually fix this

Via the AWS Console
1. Login to AWS Console (with appropriate permissions to View Identity Access
Management Account Settings)
2. Go to IAM Service on the AWS Console
22 | P a g e
3. Click on Account Settings on the Left Pane
4. Set "Minimum password length" to 14 or greater.
5. Click "Apply password policy"
Via CLI
```
aws iam update-account-password-policy  --minimum-password-length 14
```
**Note:** All commands starting with "aws iam update-account-password-policy" can be
combined into a single command.
