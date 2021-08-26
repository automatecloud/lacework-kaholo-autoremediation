# AutoRemediation for the Lacework Policy LW_S3_13

## Description
Ensure the S3 bucket has access logging enabled

Access logging provides records of requests that are made to a bucket. Access log information is
useful in security investigations and may be required for audit purposes. It is good practice review
bucket objects and enable server access logging as appropriate.

**Rationale:**
If the S3 bucket has access logging enabled, you will be able to track every request made to
access the bucket. Monitoring this activity can be used to detect anomalies and protect against
unauthorized access.

### Severity
Low

### Control ID
LW_S3_13

### Remediation Steps to manually fix this

Perform the following to enable server access logging:
1. Sign in to the AWS Management Console
2. Open the S3 Service - https://console.aws.amazon.com/s3/
3. Select S3 bucket you want to change
4. Navigate to the ‘Properties’ panel
5. Select the ‘Server access logging’ box
6. Check ‘Enable logging’
7. Provide the name of the target bucket where the events will be logged
8. Provide the target prefix to provide a sub-directory within the bucket where the log will be
stored
9. Click ‘Save’ to enable logging
10. Repeat steps 3-9 for every bucket for which you want to audit s3 activity

## How can i use this Map for Auto Remediation?

We recommend to create an S3 test bucket. This test bucket will have by default the bucket logging disabled. It will generate an event and alert inside Lacework during the next compliance check. By default the compliance check is done once per day (every 24 hours). You can force to create a compliance check for CIS Benchmarks via the Lacework GUI or the API. Out of the compliance check an Event will be generated can then be used to test the Auto Remediation of this Map.

**Note:** Make sure you configure the **YOURBUCKETNAME** with the name of the S3 test bucket you would like to use for tests. Don't use any S3 bucket with important data! This if for testing of this map only and it should not have any important data.

## Import the Map

The Map needs to be imported inside an existing or new Kaholo Project.

### Map Design and workflow
The **LW_S3_13** map currently has the following map design:

<img src="LW_S3_13.png">


* The map will start with the **Get event details** object when it was triggered by the [Lacework Trigger](https://github.com/Kaholo/kaholo-trigger-lacework). It will use the **event_id** send by the [Webhook payload](https://support.lacework.com/hc/en-us/articles/360034367393-Webhook), using the **Lacework API Access Key(s)** and  **Lacework Secret Key(s)** from the Kaholo vault that you used to configure the [Lacework Plugin](https://github.com/Kaholo/kaholo-plugin-lacework) to connect to the API. The Method **Get event details** will create a [temporary API token](https://support.lacework.com/hc/en-us/articles/360011403853-Generate-API-Access-Keys-and-Tokens). This token is used to query the [Lacework API](https://lwcs.lacework.net/api/v1/external/docs) via the API call **/api/v1/external/events/GetEventDetails** of the configured [Lacework Plugin](https://github.com/Kaholo/kaholo-plugin-lacework) host instance. The return value of this API call is the complete Event Payload you can use within the Map.
* The map will start with the **Get report details** object when the map was manually started by a user of the map. It will use the **Lacework API Access Key(s)** and  **Lacework Secret Key(s)** from the Kaholo vault that you used to configure the [Lacework Plugin](https://github.com/Kaholo/kaholo-plugin-lacework). The Method **GetLatestAWSComplianceReportDetails** will create a [temporary API token](https://support.lacework.com/hc/en-us/articles/360011403853-Generate-API-Access-Keys-and-Tokens). This token is used to query the [Lacework API](https://lwcs.lacework.net/api/v1/external/docs) via the API call **/api/v1/external/compliance/aws/GetLatestComplianceReport** for the **reporttype** of the **LaceworkConfig**  configured [Lacework Plugin](https://github.com/Kaholo/kaholo-plugin-lacework) host instance that is using the **aws_account_id** of the **LaceworkConfig** as a parameter.
* The map will trigger the **Delete Bucket Policy via CLI** CommandLine object If you enabled the Auto Remediation inside the LaceworkConfig of the map by using the **"dothedeletebucketpolicyremediationviacli": "true"** setting. It will print out the name of the S3 buckets that will be remediated, creates a backup of the current bucket policy of each S3 bucket inside the folder **backupfolder** of the LaceworkConfig and uses the AWS CLI to delete the Bucket Policy of the S3 buckets affected.
* The map will trigger the **Create Backup via CLI**, **Create the news JSON file** and  **Replace Bucket Policy via CLI** CommandLine object If you enabled the Auto Remediation inside the LaceworkConfig of the map by using the **"dothereplacebucketpolicyremediationviacli": "true"** setting. It will print out the name of the S3 buckets that will be remediated, creates a backup of the current bucket policy of each S3 bucket inside the folder **backupfolder** of the LaceworkConfig, uses the Kaholo TextEditor Object to create a new Bucket Policy inside the **inputfolder** of the LaceworkConfig and uses the AWS CLI to put the new bucket policy of the JSON file to the S3 buckets affected.
* The map will trigger the **Backup Bucket Policy via Object** and **Delete Bucket Policy via Object option** Amazon-aws-s3 object If you enabled the Auto Remediation inside the LaceworkConfig of the map by using the **"dothedeletebucketpolicyremediationviaobject": "true"** setting. It will remediate all S3 buckets by first creating a Backup of the Bucket Policy using the Method **"Get Bucket Policy"** from the [S3 bucket plugin](https://github.com/Kaholo/kaholo-plugin-amazon-s3). After that it will delete the bucket policy of the S3 bucket by using the Method **"Delete Bucket Policy"** from the [S3 bucket plugin](https://github.com/Kaholo/kaholo-plugin-amazon-s3).
* The map will trigger the **Backup Bucket Policy via Object**, **Create the new JSON** and **Replace Bucket Policy via Object option** Amazon-aws-s3 object If you enabled the Auto Remediation inside the LaceworkConfig of the map by using the **"dothereplacebucketpolicyremediationviaobject": "true"** setting. It will remediate all S3 buckets by first creating a Backup of the Bucket Policy using the Method **"Get Bucket Policy"** from the [S3 bucket plugin](https://github.com/Kaholo/kaholo-plugin-amazon-s3). After that it will create a new Bucket Policy JOSN file for documentation by using the [Text Editor plugin](https://github.com/Kaholo/kaholo-plugin-textEditor) The last object will delete the bucket policy of the S3 bucket by using the Method **"Delete Bucket Policy"** from the [S3 bucket plugin](https://github.com/Kaholo/kaholo-plugin-amazon-s3).
* The map will trigger the **Put Bucket Tags via Object** object if you configured the **putbuckettaggingviaobject** of the **LaceworkConfig** equals **true**. It will use the **tagname** and **tagvalue** to put these tags for every bucket that is in violation with the rule and ignored via the **bucketIgnoreList** of the **LaceworkConfig**.
* The map will trigger the **Put Bucket Tags via CLI** object if you configured the **putbuckettaggingviacli** of the **LaceworkConfig** equals **true**. It will use the **tagname** and **tagvalue** to put these tags for every bucket that is in violation with the rule and ignored via the **bucketIgnoreList** of the **LaceworkConfig**.
* The map will send out a Slack message for each S3 bucket that will be remediated to the Webhook you configured by using the **Remediated** Slack object.
* If you enabled the configuration to send out slack messages for ignored S3 buckets inside the LaceworkConfig of the map to **"sendslackmessagesforignored": "true"** it will send out a slack message for each bucket that is violating the policy and ignored by the configuration to the Webhook you configured for the **Ignored** Slack object.
* The map will trigger the **Get current suppression configuration** if you configured the **configuresuppressiononpolicy** equals **true**. It will read out the current suppression configuration for the **rec_id** and reconfigure it with the object **Configure Suppression via Tags** to the configuration **tagname**, **tagvalue** and **suppressionpolicycomment** if the current tag name is not equal **tagname** and/or the current tag value is not equal **tagvalue**.

### Map trigger

Make sure that the Map Webhook Trigger is configured with the following configuration:

<img src="LW_S3_13_Trigger.png" width="361" height="810">

1. The Configuration setting needs to be configured with **LaceworkConfig** to make sure the Configuration **LaceworkConfig** is used when the map is triggered.
2. The Plugin setting needs to be configured with the Lacework Webhook Plugin **kaholo-trigger-lacework**
3. For the Method setting you need to select **Lacework Alert**
4. The Variable **Event type** needs to be configured with Value **Compliance**
5. The Variable **Event ID** needs to be configured with Value **LW_S3_13**.
6. The Variable **Event Severity** needs to be configured with the Value **Any** or **High**
7. Make sure to enable the Checkbox **Include Higher Severities**.

This configuration will make sure that this map is only triggered if the **rec_id** of the [Webhook payload](https://support.lacework.com/hc/en-us/articles/360034367393-Webhook) is equal to the **LW_S3_13** Event ID.

### Configuration of the Map

By default the map is using the **LaceworkConfig** configurations that are imported as part of the map.

By default the map has the following configurations:

```
{
    "name": "LaceworkConfiguration",
    "policyID": "LW_S3_13",
    "violationdescription": "Ensure the S3 bucket has access logging enabled",
    "eventuuid": "42bb48ed-ae0a-4093-854d-2dc6777f618d",
    "reportuuid": "a6d14793-6dd4-4d22-8cc8-9d49edd6fd2a",
    "enablebucketloggingviacli": "false",
    "enablebucketloggingviaobject": "false",
    "sendslackmessagesforignored": "true",
    "bucketIgnoreList": [
        "arn:aws:s3:::mybucket01",
        "arn:aws:s3:::mybucket02",
        "arn:aws:s3:::mybucket03"
    ],
    "awsaccountid": "123456789012",
    "reporttype": "AWS_CIS_S3",
    "putbuckettaggingviacli": "true",
    "putbuckettaggingviaobject": "false",
    "tagname": "LW_S3_13",
    "tagvalue": "suppressed",
    "autoremediationonlyfornewviolations": "false",
    "inputfolder": "/usr/src/app/scripts/input/",
    "loggingconfiguration": {
        "LoggingEnabled": {
            "TargetBucket": "myBucket",
            "TargetPrefix": "MyBucketLogs/",
            "TargetGrants": [
                {
                    "Grantee": {
                        "Type": "Group",
                        "URI": "http://acs.amazonaws.com/groups/s3/LogDelivery"
                    },
                    "Permission": "WRITE"
                },
                {
                    "Grantee": {
                        "Type": "Group",
                        "URI": "http://acs.amazonaws.com/groups/s3/LogDelivery"
                    },
                    "Permission": "READ_ACP"
                }
            ]
        }
    }
}
```
Make sure you configure the following configurations inside the **LaceworkConfig** Configuration of the map

#### General Settings


1. **eventuuid:** Make sure that the **uuid** used here is the uuid of the **Get event details** object inside the map. Due to the reimport of the Map the **uuid** of the event object could have changed. To check the uuid you can go to the Design of the map, open the **Get event details** building block.

![Get Event](geteventdetails.png "Get Event")

Inside the configuration of the **Get event details** building block you will find the **uuid**:

![Get Event Details](geteventdetails2.png "Get Event")

2. **reportuuid:** Make sure that the **uuid** used here is the uuid of the **Get report details** object inside the map. Due to the reimport of the Map the **uuid** of the event object could have changed. To check the uuid you can go to the Design of the map, open the **Get report details** building block.

![Get Event](getreportdetails.png "Get Event")

Inside the configuration of the **Get report details** building block you will find the **uuid**:

![Get Report Details](getreportdetails2.png "Get Event")

3. **bucketIgnoreList(Optional):** You can configure the Map to ignore specific S3 buckets from Auto Remediation. Make sure you configured the correct AWS S3 bucket names that should be ignored within the **bucketIgnoreList** of the **LaceworkConfig**.

4. **putbuckettaggingviacli**: If you configure this settings to **true** it will add the **tagname** and **tagvalue** for each S3 bucket that is ignored via the **bucketIngoreList** by using the AWS CLI. This can be helpful to configure the policy to suppress every S3 bucket that is having this **tagname** and **tagvalue** as advanced suppression configured.

If you enabled it the following AWS CLI command will be used to add the tag to the S3 bucket:
```
aws resourcegroupstaggingapi tag-resources --resource-arn-list <ARNOFYOURYOURBUCKETNAME> --tags <TAGNAME>=<TAGVALUE> --profile AWS-ACCOUNTID-FROM-EVENTORREPORT
```
If you want to know more about the aws resourcegroupstaggingapi tag-resources command or want to replace it with a different option for auto remediation we recommend to take a look at the official documentation available [here](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/resourcegroupstaggingapi/tag-resources.html).

For the command to execute successful it is important that you add the AWS Account ID with the id of the account as a profile to your aws cli.

5. **putbuckettaggingviaobject**: If you configure this settings to **true** it will add the **tagname** and **tagvalue** for each S3 bucket that is ignored via the **bucketIngoreList** by using the [Kaholo AWS Resource Groups tagging Plugin](https://github.com/Kaholo/kaholo-plugin-aws-resource-groups-tagging). This can be helpful to configure the policy to suppress every S3 bucket that is having this **tagname** and **tagvalue** as advanced suppression configured.

6. **reporttype**: You can define the Report Type the Map should run against, you can choose between:
  * **AWS_CIS_S3** (AWS CIS Benchmark and S3 Report)
  * **NIST_800-53_Rev4** (AWS NIST 800-53 Report)
  * **NIST_800-171_Rev2** (AWS NIST 800-171 Report)
  * **ISO_2700** (AWS ISO27001:2013 Report)
  * **HIPAA** (AWS HIPAA Report)
  * **SOC** (AWS SOC2 Report)

#### Auto Remediation

For the Auto Remediation you need to decide if you would like to Auto Remediate by using the AWS CLI or the Kaholo S3 Bucket Object.

The Auto Remediation is disabled if you import the map. It will only be triggered if the configuration **dothedeletebucketpolicyremediationviacli**,**dothedeletebucketpolicyremediationviaobject**, **dothereplacebucketpolicyremediationviacli**  or **dothereplacebucketpolicyremediationviaobject** of the LaceworkConfig is configured with **true**. Before enabling this we recommend the following:

1. Create a test S3 bucket that is violating the compliance rule for **LW_S3_13** via the CLI command described in the section [How can i use the Map?](https://github.com/automatecloud/lacework-kaholo-autoremediation/tree/main/maps/compliance/aws/LW_S3_13#how-can-i-use-this-map-for-auto-remediation)
2. When you got the Event created in Lacework you need to make sure that you put all the S3 bucket names that should not be Auto Remediated into the bucketIgnoreList of the LaceworkConfig.
3. To be even more sure we recommend to configure a suppression setting for the **LW_S3_13** compliance check within the Lacework platform to ignore the S3 bucket. Otherwise the ignored Buckets will create additional Events and Alerts within Lacework. Future versions of this Map will enable the auto creation of AWS Tags.
4. After that you can enable the Auto Remediation via CLI or via the Kaholo S3 Bucket Object.

**Note:** you can choose to do the Auto Remediation via the CLI or by using the Kaholo S3 bucket object. By default all four Auto Remediation settings are configured to **false**, so it will not by accident start to remediate misconfigured S3 buckets. We recommend to make sure that only the right buckets will be remediated and the map is working as expected before you configure any of both settings to true. Do not configure more then one of the auto remediations available at the same time to **true**. The map will check that possible misconfiguration at the beginning of the map and not execute. Only one of both can be enabled and used for the Auto Remediation.

5. If you configure the **enablebucketloggingviacli** settings to **true** to enable the Auto Remediation via CLI, make sure you select an Agent for the Map that has the AWS CLI installed and configured. The Remediation via CLI block will Auto Remediate by first preparing the target bucket with the right access. It will use the following AWS CLI command:

```
aws s3api put-bucket-acl --bucket <YOURBUCKETNAME> --grant-write URI=http://acs.amazonaws.com/groups/s3/LogDelivery --grant-read-acp URI=http://acs.amazonaws.com/groups/s3/LogDelivery`
```

If you want to know more about the aws s3api put-bucket-acl command or want to replace it with a different option for auto remediation we recommend to take a look at the official documentation available [here](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/put-bucket-acl.html).

After preparing the target bucket for logging it will use the [Text Editor plugin](https://github.com/Kaholo/kaholo-plugin-textEditor) to create a new logging JSON file.

That new JSON file will be used to configure the Logging of the S3 Bucket via the following AWS CLI command:

```
aws s3api put-bucket-logging --bucket <YOURBUCKETNAME> --bucket-logging-status file://bucketname-LW_S3_13.json
```

If you want to know more about the aws s3api put-bucket-logging command or want to replace it with a different option for auto remediation we recommend to take a look at the official documentation available [here](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/put-bucket-logging.html).

6. If you configure the **enablebucketloggingviaobject** to **true** the Auto Remediation is done by using the [S3 bucket plugin](https://github.com/Kaholo/kaholo-plugin-amazon-s3) using the Methods **"Manage Bucket ACL"** for the target bucket and **"Manage Bucket Logging"** for the S3 bucket itself.

#### Configuration of Slack Messages

1. **policyID:** This shouldn't be changed. The Policy ID will be shown as part of the slack output messages. And it will be used as part of the name of the JSON Backups and Input files for the S3 buckets.

2. **violationdescription:** This setting is used to send details about the event inside the slack output message. Feel free to change it for your needs.

3. For the Slack building blocks **Remediated** and **Ignored** you can configure a Slack Webhook URL that you have to implement inside the Kaholo Vault before you can select it.

It will send out a slack message to the configured Webhook. We recommend to configure it similar to the Webhook you use within Lacework as an alert channel so you can see the Auto Remediation effect right after the alert was send by Lacework.

If you don't have Slack or don't need Slack messages feel free to simply remove both Slack objects from your map.

4. **sendslackmessagesforignored (Optional):** you can disable within the LaceworkConfig via **"sendslackmessagesforignored": "false"** to not send out Slack messages for S3 buckets that are violating the policy but are ignored via the **bucketIgnoreList**. By default this is configured to **true**. Reason behind is that it is best practice to suppress S3 buckets that should not be Auto Remediated by using Tags within AWS so you can configure a Suppress rule within Lacework to simply ignore them and not create events and alerts.

5. If you configure the **autoremediationonlyfornewviolations** equals true the Auto Remediation will only be done for new Resource Violations on S3 buckets within new Events. With that you avoid that the AutoRemedation is doing it for all (new and already existing violations) of S3 buckets. This doesn't have any effect if you do the AutoRemedation via Reports, as reports have no differences between new and already existing violating resources. By default this setting is configured equals **false**.

#### Configuration of Slack Messages

1. **policyID:** This shouldn't be changed. The Policy ID will be shown as part of the slack output messages. And it will be used as part of the name of the JSON Backups and Input files for the S3 buckets.

2. **violationdescription:** This setting is used to send details about the event inside the slack output message. Feel free to change it for your needs.

3. For the Slack building blocks **Remediated** and **Ignored** you can configure a Slack Webhook URL that you have to implement inside the Kaholo Vault before you can select it.

It will send out a slack message to the configured Webhook. We recommend to configure it similar to the Webhook you use within Lacework as an alert channel so you can see the Auto Remediation effect right after the alert was send by Lacework.

If you don't have Slack or don't need Slack messages feel free to simply remove both Slack objects from your map.

4. **sendslackmessagesforignored (Optional):** you can disable within the **LaceworkConfig** via the setting equals **false** to not send out Slack messages for S3 buckets that are violating the policy but are ignored via the **bucketIgnoreList**. By default this is configured to **true**. Reason behind is that it is best practice to suppress S3 buckets that should not be Auto Remediated by using Tags within AWS so you can configure a Suppress rule within Lacework to simply ignore them and not create events and alerts. You can use the setting **putbuckettaggingviacli** or **putbuckettaggingviaobject** to add the **tagname** and **tagvalue** for each S3 bucket that is ignored.

## Build an example curl webhook

There is no need to wait for Lacework sending the Webhook Alert for the generated Event when you want to test the map. If you plan to test it immediately, you can trigger the map by using a simple curl command that will send the necessary information.

Before you can trigger the webhook you need to have an event generated within your Lacework instance. Please make sure you run a compliance report right after you created a test S3 bucket that is violating this policy.

As soon as you got an event we recommend using the Event Information to create an example webhook trigger inside your terminal using the following environment variables. Make sure to update it with the information from the Event you did generate.#

```
export EVENTTITLE="New Violations"
export EVENTTYPE=Compliance
export EVENTTIMESTAMP="27 Jan 2021 16:00 GMT"
export EVENTSOURCE=AWSCompliance
export EVENTID=11
export EVENTSEVERITY=1
export WEBHOOKURL=https://mykaholoinstance.kaholo.io/webhook/lacework/alert
export LACEWORKINSTANCE=mylaceworkinstance
export EVENTDESCRIPTION="AWS Account 112233445566 (lacework-test) : LW_S3_13 Ensure the S3 bucket has access logging enabled"
```

You need to replace the following before you apply the environment variables:
1. **EVENTID** with the EventID that was generated inside the Lacework environment.
2. **WEBHOOKURL** with your Kaholo Webhook Url. Normally kaholo is listening on port 3000 and the URL path for the webhook alerting is /webhook/lacework/alert.
3. **LACEWORKINSTANCE** your Lacework instance where you created that event.
4. **EVENTDESCRIPTION** replace the AWS Account with your environment specific AWS Account ID.

With that you can trigger the webhook inside kaholo by using the following curl command:

```
curl -X POST -H 'Content-type: application/json' --data '{"event_title": "'"$EVENTTITLE"'", "event_link": "https://'"$LACEWORKINSTANCE"'.lacework.net/ui/investigation/recents/EventDossier-'"$EVENTID"'", "lacework_account": "'"$LACEWORKINSTANCE"'", "event_source": "'"$EVENTSOURCE"'", "event_description":"'"$EVENTDESCRIPTION"'", "event_timestamp":"'"$EVENTTIMESTAMP"'", "event_type": "Compliance", "event_id": "'"$EVENTID"'", "event_severity": "'"$EVENTSEVERITY"'"}' $WEBHOOKURL
```
We recommend to check the Execution Results when you give it a try. With that you make sure it will remediate the right S3 buckets before you enable the auto remediation.

## AWS accounts and required AWS permissions (least privilege)

The Map supports multiple AWS accounts for events send by Lacework. You need to make sure that you saved your AWS account access keys and the AWS secret access keys in the following format:

* **AWS-ACCOUNT-ACCESS-KEY-ID_aws_access_key_id**: example 12345678912_aws_access_key_id
* **AWS-ACCOUNT-SECRET-ACCESS-KEY-ID_aws_secret_access_key_id**: example 12345678912_aws_secret_access_key_id

We recommend to use the Map with the principals of least privilege to make sure the Auto Remediation account can only change the S3 Bucket ACL and the Resource Tags.

The Map is using the API call put-bucket-acl to put the bucket acl for the target bucket that will be used for sending the logging information.

```
aws s3api put-bucket-acl --bucket <YOURBUCKETNAME> --grant-write URI=http://acs.amazonaws.com/groups/s3/LogDelivery --grant-read-acp URI=http://acs.amazonaws.com/groups/s3/LogDelivery`
```
The Map also is using the API call put-bucket-logging to configure logging of the S3 bucket.

```
aws s3api put-bucket-logging --bucket <YOURBUCKETNAME> --bucket-logging-status file://bucketname-LW_S3_13.json
```

And also the resource group tagging api to add the necessary tags to the S3 bucket:

```
aws resourcegroupstaggingapi tag-resources --resource-arn-list <ARNOFYOURYOURBUCKETNAME> --tags <TAGNAME>=<TAGVALUE> --profile AWS-ACCOUNTID-FROM-EVENTORREPORT
```

You need to define the following least privilege policy inside your AWS IAM configuration for the service account used to do the auto remediation:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:GetBucketTagging",
                "s3:PutBucketTagging",
                "tag:GetTagValues",
                "s3:PutBucketLogging",
                "s3:GetBucketLogging",
                "tag:GetTagKeys",
                "tag:TagResources"
            ],
            "Resource": "*"
        }
    ]
}
```

## What features are supported with this Map? Release Notes

The Map Version 1.0 (10th of May 2021) supports the following:
* Auto Remediation via the [AWS Command Line Interface](https://aws.amazon.com/cli/)
* Auto Remediation via the [Kaholo S3 bucket plugin](https://github.com/Kaholo/kaholo-plugin-amazon-s3)
* Adding S3 Bucket Tags for Advanded Suppression via the [AWS Command Line Interface](https://aws.amazon.com/cli/)
* Adding S3 Bucket Tags for Advanded Suppression via the [Kaholo AWS Resource Groups tagging Plugin](https://github.com/Kaholo/kaholo-plugin-aws-resource-groups-tagging)
* Ignoring S3 Buckets from Auto Remediation.
* Auto Remediation via Lacework Events.
* Auto Remediation via Lacework Compliance reports.
* Auto Remediation for only new compliance violations.
* Sending Slack messages via the [Kaholo Slack Plugin](https://github.com/Kaholo/kaholo-plugin-slack) for S3 Buckets that will be remediated.
* Sending Slack messages via the [Kaholo Slack Plugin](https://github.com/Kaholo/kaholo-plugin-slack) for S3 Buckets that will be ignored.
* Not sending Slack messages for S3 Buckets that will be ignored.
* Support for multiple AWS account ids used for the AWS CLI and Kaholo Plugins.
* Define the report that it should run against.
* Using least privilege permissions in AWS.

## Ideas for future releases

* Adding Advanded Suppression inside Lacework (as soon as the API is available.)
* Adding Auto Remediation example with Lambda functions
* Adding Auto Remediation example with terraform
* Adding Auto Remediation example with pulumi
