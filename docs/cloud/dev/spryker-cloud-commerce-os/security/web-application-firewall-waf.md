---
title: Web Application Firewall (WAF)
description: WAF protects your SCCOS applications from web exploits and bots.
template: concept-topic-template
---

AWS WAF is a web application firewall that helps protect your web applications or APIs against common web exploits, SQL injections, cross-site scripting, or bots that may affect availability, compromise security, or consume excessive resources.

For more information on WAF, see [AWS WAF](https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html).

WAF protects your SCCOS applications using a set of pre-defined rules. When web request triggers a rule, WAF blocks it. Occasionally, you will be getting false positives. Usually, in a web application, a false positive results into error 403. If you get the error, troubleshoot it by following [Tutorial — Troubleshooting 403 error](/docs/cloud/dev/spryker-cloud-commerce-os/troubleshooting/troubleshooting-tutorials/tutorial-troubleshooting-403-error.html).
