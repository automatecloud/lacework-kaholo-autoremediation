# lacework-kaholo-autoremediation

This repository is a collection of [Kaholo.io](https://www.kaholo.io) maps you can use as examples to automate the remediation of [Lacework](https://www.lacework.com/) alerts.

## What is auto remediate?
Auto remediation is the idea to automate responds to events with automated steps that are able to fix, or remediate, underlying conditions without the need of interaction from anyone. Auto remediation itself can be triggering a CLI command, a serverless function or an API call to remediate Alerts detected by Lacework. Automation of Remediation can be easy or complex depending on the alert and context correlated with the necessary remediation steps.

## Why should i use auto remediation?
We live in a complex world of Multi Cloud Environments. Cloud itself isn't as easy as it was sold to us. With the adoption of cloud and cloud native applications using modern technology like Kubernetes, Container and Serverless applications you automatically adopt endless complexity with many potential security risks. All of the services need to fulfill your security and compliance regulations. Your target should be to secure as much and as best as possible, independent of the industry and compliance regulations you need to fulfill.

Auto remediation means to automate the necessary steps of alert events detected by Lacework without any human interaction. Auto Remediation can partially or fully help to fix specific alerts.

Simplified you can say: "The more is automated, the faster you can react to alerts and the more time you safe for doing any manual interactions". Time is money and in security it means a risk you take while the alert is not solved. The MTTR (Mean Time to Repair) should be as fast as possible to not take any risks for a long time in case of an alert.

## Why Lacework and Kaholo?
Lacework and Kaholo is a perfect match!

Lacework itself is using Data ware house technology (Snowflake) and Machine Learning technology to reduce the number of false positive events and create high quality alerts (events). These Alerts from Lacework in general have a lot of high quality context information included that can be used to automate the necessary remediation steps.

Kaholo is an easy and intuitive workflow engine that makes it easy to create almost any automation processes, including advanced ones. On top of that you get central visibility into all automation processes. Instead of simply triggering a single CLI command or single API calls and serverless functions it allows the creation of complex workflows that might be necessary for specific auto remediation steps.

## How does it work?
The integration between Lacework and Kaholo is done by using the Alert Webhook channel. https://support.lacework.com/hc/en-us/articles/360034367393-Webhook.

The Webhook Alert sends all the necessary information to the Kaholo Lacework Webhook 

Least Privilege
