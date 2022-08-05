---
title: Demo data was imported incorrectly
description: Learn how to fix the issue when demo data was imported incorrectly
last_updated: Jun 16, 2021
template: troubleshooting-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/demo-data-was-imported-incorrectly
originalArticleId: 49e90c4b-9c36-4d31-af99-c48dc9d0b412
redirect_from:
  - /2021080/docs/demo-data-was-imported-incorrectly
  - /2021080/docs/en/demo-data-was-imported-incorrectly
  - /docs/demo-data-was-imported-incorrectly
  - /docs/en/demo-data-was-imported-incorrectly
  - /v6/docs/demo-data-was-imported-incorrectly
  - /v6/docs/en/demo-data-was-imported-incorrectly
related:
  - title: An error during front end setups
    link: docs/scos/dev/troubleshooting/troubleshooting-spryker-in-docker-issues/troubleshooting-docker-installation/an-error-during-front-end-setup.html
  - title: Docker daemon is not running
    link: docs/scos/dev/troubleshooting/troubleshooting-spryker-in-docker-issues/troubleshooting-docker-installation/docker-daemon-is-not-running.html
  - title: docker-sync cannot start
    link: docs/scos/dev/troubleshooting/troubleshooting-spryker-in-docker-issues/troubleshooting-docker-installation/docker-sync-cannot-start.html
  - title: Error 403 No valid crumb was included in the request
    link: docs/scos/dev/troubleshooting/troubleshooting-spryker-in-docker-issues/troubleshooting-docker-installation/error-403-no-valid-crumb-was-included-in-the-request.html
  - title: Node Sass does not yet support your current environment
    link: docs/scos/dev/troubleshooting/troubleshooting-spryker-in-docker-issues/troubleshooting-docker-installation/node-saas-does-not-yet-support-your-current-environment.html
  - title: Setup of new indexes throws an exception
    link: docs/scos/dev/troubleshooting/troubleshooting-spryker-in-docker-issues/troubleshooting-docker-installation/setup-of-new-indexes-throws-an-exception.html
  - title: Vendor folder synchronization error
    link: docs/scos/dev/troubleshooting/troubleshooting-spryker-in-docker-issues/troubleshooting-docker-installation/vendor-folder-synchronization-error.html
---

## Description

Demo data was imported incorrectly.

## Solution

Re-load the demo data:

```bash
docker/sdk clean-data && docker/sdk up --data && docker/sdk console q:w:s -v -s
```
