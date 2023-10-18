---
title: Install in Demo mode on MacOS and Linux
description: Learn how to install Spryker in Demo mode on MacOS and Linux.
last_updated: Jul 5, 2022
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/installing-in-demo-mode-on-macos-and-linux
originalArticleId: 3b78ae4c-d2a3-4dfa-87e1-7d0c4096ee22
redirect_from:
  - /2021080/docs/installing-in-demo-mode-on-macos-and-linux
  - /2021080/docs/en/installing-in-demo-mode-on-macos-and-linux
  - /docs/installing-in-demo-mode-on-macos-and-linux
  - /docs/en/installing-in-demo-mode-on-macos-and-linux
  - /v6/docs/installing-in-demo-mode-on-macos-and-linux
  - /v6/docs/en/installing-in-demo-mode-on-macos-and-linux
  - /v5/docs/installation-guide-demo-mode
  - /v5/docs/en/installation-guide-demo-mode
  - /v4/docs/installation-guide-demo-mode
  - /v4/docs/en/installation-guide-demo-mode
  - /v3/docs/spryker-in-docker-dev-mode-201907
  - /v3/docs/en/spryker-in-docker-dev-mode-201907
  - /docs/scos/dev/setup/installing-spryker-with-docker/installation-guides/installing-in-demo-mode-on-macos-and-linux.html
related:
  - title: Database access credentials
    link: docs/scos/dev/set-up-spryker-locally/set-up-spryker-locally.html
---

{% info_block infoBox "" %}

Starting with the 202204.0 release, the following guide applies to both Intel and ARM architectures. You can install the demo shops of previous versions on ARM chips by following [Switch to ARM architecture](/docs/scos/dev/technical-enhancement-integration-guides/switch-to-arm-architecture-m1-chip.html).

{% endinfo_block %}


This document describes how to install Spryker in [Demo Mode](/docs/scos/dev/set-up-spryker-locally/install-spryker/install/choose-an-installation-mode.html#demo-mode) on MacOS and Linux.

## Install Docker prerequisites on MacOS and Linux

* [Install Docker prerequisites on MacOS](/docs/scos/dev/set-up-spryker-locally/install-spryker/install-docker-prerequisites/install-docker-prerequisites-on-macos.html)
* [Install Docker prerequisites on Linux](/docs/scos/dev/set-up-spryker-locally/install-spryker/install-docker-prerequisites/install-docker-prerequisites-on-linux.html)

## Clone a Demo Shop and the Docker SDK

1. Open a terminal.
2. Clone *one* of the following Demo Shops and navigate into its folder:

    * B2C Demo Shop:

    ```shell
    git clone https://github.com/spryker-shop/b2c-demo-shop.git -b 202307.0 --single-branch ./b2c-demo-shop && \
    cd b2c-demo-shop
    ```

    * B2B Demo Shop:

    ```shell
    git clone https://github.com/spryker-shop/b2b-demo-shop.git -b 202307.0 --single-branch ./b2b-demo-shop && \
    cd b2c-demo-shop
    ```

    * B2C Marketplace Demo Shop

    ```shell
    git clone https://github.com/spryker-shop/b2c-demo-marketplace.git -b 202307.0 --single-branch ./b2c-demo-marketplace && \
    cd b2c-demo-marketplace
    ```

    * B2B Marketplace Demo Shop

    ```shell
    git clone https://github.com/spryker-shop/b2b-demo-marketplace.git -b 202307.0 --single-branch ./b2b-demo-marketplace && \
    cd b2b-demo-marketplace
    ```    

3. Clone the Docker SDK:

```shell
git clone https://github.com/spryker/docker-sdk.git --single-branch docker
```

## Configure and start the instance


1. Bootstrap the local Docker setup for demo:

```shell
docker/sdk bootstrap
```

{% info_block warningBox "Bootstrap" %}

Once you finish the setup, you don't need to run `bootstrap` to start the instance. You only need to run it after updating the Docker SDK or changing the deploy file.

{% endinfo_block %}


2. Update the hosts file using the command provided in the output of the previous step. It should be similar to the following:

![update-hosts](https://spryker.s3.eu-central-1.amazonaws.com/docs/scos/dev/setup/quickstart-guides-install-spryker/quickstart-guide-install-spryker-on-macos-and-linux/update-hosts.png)


3. Build and start the instance:

```shell
docker/sdk up
```

Depending on the hardware performance, the first project launch can take up to *20 minutes*.

## Endpoints

To ensure that the installation is successful, make sure you can access the configured endpoints from the Deploy file. For more information about the Deploy file, see [Deploy file reference - 1.0](/docs/scos/dev/the-docker-sdk/{{site.version}}/deploy-file/deploy-file-reference-1.0.html).

## Back-Office

The default credentials to access the Back Office are located inside `/src/Pyz/Zed/User/UserConfig.php`.

## RabbitMQ

To access RabbitMQ UI, use `spryker` as a username and `secret` as a password. You can adjust the credentials in `deploy.yml`. For information about the Deploy file, see [Deploy file reference - 1.0](/docs/scos/dev/the-docker-sdk/{{site.version}}/deploy-file/deploy-file-reference-1.0.html).

## Get the list of useful commands

To get the full and up-to-date list of commands, run `docker/sdk help`.

## Next steps

* [Troubleshooting](/docs/scos/dev/set-up-spryker-locally/troubleshooting-installation/troubleshooting-installation.html)
* [Configuring debugging in Docker](/docs/scos/dev/the-docker-sdk/{{site.version}}/configuring-debugging-in-docker.html)
* [Deploy file reference - 1.0](/docs/scos/dev/the-docker-sdk/{{site.version}}/deploy-file/deploy-file-reference-1.0.html)
* [Configuring services](/docs/scos/dev/the-docker-sdk/{{site.version}}/configure-services.html)
* [Set up a self-signed SSL certificate](/docs/scos/dev/set-up-spryker-locally/configure-after-installing/set-up-a-self-signed-ssl-certificate.html)
