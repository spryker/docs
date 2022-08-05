---
title: DevVM system requirements
description: This article provides the configuration that a system must have in order for the Spryker project to run smoothly and efficiently.
last_updated: Jun 16, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/system-requirements
originalArticleId: 6f7d36c1-2ee4-47d1-8f7f-ea0f1b7f93a7
redirect_from:
  - /2021080/docs/system-requirements
  - /2021080/docs/en/system-requirements
  - /docs/system-requirements
  - /docs/en/system-requirements
  - /v6/docs/system-requirements
  - /v6/docs/en/system-requirements
  - /v5/docs/system-requirements
  - /v5/docs/en/system-requirements
  - /v4/docs/system-requirements
  - /v4/docs/en/system-requirements
  - /v3/docs/system-requirements
  - /v3/docs/en/system-requirements
  - /v2/docs/system-requirements
  - /v2/docs/en/system-requirements
  - /v1/docs/system-requirements
  - /v1/docs/en/system-requirements
  - /v4/docs/supported-browsers
  - /v4/docs/en/supported-browsers
  - /docs/scos/dev/setup/system-requirements.html
related:
  - title: Installing Spryker with development virtual machine
    link: docs/scos/dev/setup/installing-spryker-with-development-virtual-machine/installing-spryker-with-development-virtual-machine.html
  - title: Installing Spryker with DevVM on MacOS and Linux
    link: docs/scos/dev/setup/installing-spryker-with-development-virtual-machine/installing-spryker-with-devvm-on-macos-and-linux.html
  - title: Installing Spryker with DevVM on Windows
    link: docs/scos/dev/setup/installing-spryker-with-development-virtual-machine/installing-spryker-with-devvm-on-windows.html
---
{% info_block warningBox "Warning" %}

We will soon deprecate the DevVM and stop supporting it. Therefore, we highly recommend [installing Spryker with Docker](/docs/scos/dev/setup/installing-spryker-with-docker/installing-spryker-with-docker.html).

{% endinfo_block %}

| REQUIREMENT | VALUE |
| ----------------- | ----------------------- |
| OS                          | <ul><li>Native: Linux</li><li>DevVM: MacOS and Windows</li></ul>  |
| **Web Server**                                | NginX - preferred. But any webserver which supports PHP will work such as lighttpd, Apache, Cherokee. |
| **Databases**                             | Depending on the project, one of the databases: MariaDB >= 10.4 - preferred, PostgreSQL >=9.6, or MySQL >=5.7. |
| **PHP**                                   | Spryker supports PHP `>=7.4` with the following extensions: `curl`, `json`, `mysql`, `pdo-sqlite`, `sqlite3`, `gd`, `intl`, `mysqli`, `pgsql`, `ssh2`, `gmp`, `mcrypt`, `pdo-mysql`, `readline`, `twig`, `imagick`, `memcache`, `pdo-pgsql`, `redis`, `xml`, `bz2`, `mbstring`. The preferred version is `8.0`. See [Supported Versions of PHP](/docs/scos/user/intro-to-spryker/whats-new/supported-versions-of-php.html) for details on the supported PHP versions.|
| **SSL**                                       | For production systems, a valid security certificate is required for HTTPS. |
| **Redis**                                     | Version >=3.2, >=5.0                                                |
| **Elasticsearch**                             | Version 6.x or 7.x                                        |
| **RabbitMQ**                                  | Version 3.6+                                                 |
| **Jenkins (for cronjob management)**          | Version 1.6.x or 2.x          |
| **Graphviz (for statemachine visualization)** | 2.x                                                          |
|**Node.js**| Version >= 12.0.0 |
|**NPM**| Version >= 6.9.0 |
|**Intranet**| Back Office application (Zed) must be secured in an Intranet (using VPN, Basic Auth, IP Allowlist, DMZ, etc.) |
