---
title: Install in Development mode on Windows
description: Learn how to install Spryker in Development mode on Windows.
last_updated: Oct 21, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/installing-in-development-mode-on-windows
originalArticleId: 14368b32-4d9e-4451-9a46-ecab32966d88
redirect_from:
  - /2021080/docs/installing-in-development-mode-on-windows
  - /2021080/docs/en/installing-in-development-mode-on-windows
  - /docs/installing-in-development-mode-on-windows
  - /docs/en/installing-in-development-mode-on-windows
  - /v6/docs/installing-in-development-mode-on-windows
  - /v6/docs/en/installing-in-development-mode-on-windows
  - /docs/scos/dev/set-up-spryker-locally/installing-spryker-with-development-virtual-machine/installing-spryker-with-devvm-on-windows.html
  - /docs/scos/dev/setup/installing-spryker-with-docker/installation-guides/installing-in-development-mode-on-windows.html
related:
  - title: Database access credentials
    link: docs/scos/dev/set-up-spryker-locally/set-up-spryker-locally.html

---

This document describes how to install Spryker in [Development Mode](/docs/scos/dev/set-up-spryker-locally/install-spryker/install/choose-an-installation-mode.html#development-mode) on Windows.

## Install the prerequisites on Windows

* [Install Docker prerequisites on Windows with WSL1](/docs/scos/dev/set-up-spryker-locally/install-spryker/install-docker-prerequisites/install-docker-prerequisites-on-windows-with-wsl1.html).

* [Install Docker prerequisites on Windows with WSL2](/docs/scos/dev/set-up-spryker-locally/install-spryker/install-docker-prerequisites/install-docker-prerequisites-on-windows-with-wsl2.html).


## Clone a Demo Shop and the Docker SDK

{% info_block warningBox "Filesystems" %}

Avoid using folders under the Windows filesystem, because they have to be synced with the Ubuntu filesystem, which slows down all operations significantly.

Not recommended: `/mnt/c/Users/jdoe/Desktop/project`.

Recommended: `/home/jdoe/workspace/project`.

{% endinfo_block %}

1. Open Ubuntu.
2. Open a terminal.
3. Create a new folder and navigate into it.

4. Clone *one* of the [Demo Shops](/docs/scos/user/intro-to-spryker/intro-to-spryker.html#spryker-b2bb2c-demo-shops):

    * B2C Demo Shop:

    ```shell
    git clone https://github.com/spryker-shop/b2c-demo-shop.git -b 202212.0-p2 --single-branch ./b2c-demo-shop && \
    cd b2c-demo-shop
    ```

    * B2B Demo Shop:

    ```shell
    git clone https://github.com/spryker-shop/b2b-demo-shop.git -b 202212.0-p2 --single-branch ./b2b-demo-shop && \
    cd b2c-demo-shop
    ```

    * B2C Marketplace Demo Shop

    ```shell
    git clone https://github.com/spryker-shop/b2c-demo-marketplace.git -b 202212.0-p2 --single-branch ./b2c-demo-marketplace && \
    cd b2c-demo-marketplace
    ```

    * B2B Marketplace Demo Shop

    ```shell
    git clone https://github.com/spryker-shop/b2b-demo-marketplace.git -b 202212.0-p2 --single-branch ./b2b-demo-marketplace && \
    cd b2b-demo-marketplace
    ```

{% info_block warningBox "Verification" %}

Make sure that you are in the Demo Shop's folder by running the `pwd` command.

{% endinfo_block %}

5. Clone the Docker SDK:

```bash
git clone https://github.com/spryker/docker-sdk.git --single-branch docker
```

## Configure and start the instance


1. In `{shop_name}/docker/context/php/debug/etc/php/debug.conf.d/69-xdebug.ini`, set `xdebug.remote_host` and `xdebug.client_host` to `host.docker.internal`:

```text
...
xdebug.remote_host=host.docker.internal
...
xdebug.client_host=host.docker.internal
```

2. Add your user to the `docker` group:

```bash
sudo usermod -aG docker $USER
```

3. Bootstrap local docker setup:

```bash
docker/sdk bootstrap deploy.dev.yml
```

{% info_block infoBox "Bootstrap" %}

Once you finish the setup, you don't need to run `bootstrap` to start the instance. You only need to run it after updating the Docker SDK or changing the deploy file.

{% endinfo_block %}

4. Update the hosts file based on the output of the previous step:
    1. Open the Start menu.
    2. In the search field, enter `Notepad`.
    3. Right-click **Notepad** and select **Run as administrator**.
    4. In the **User Account Control** window, select **Yes** to confirm the action.
    5. In the upper navigation panel, click **File** > **Open**.
    6. Put the following path into the address line: `C:\Windows\System32\drivers\etc`.
    7. In the **File name** line, enter `hosts` and select **Open**.
    The hosts file opens in the drop-down.
    8. Add the entries provided in the outpout of the `bootstrap` command.

    {% info_block warningBox "Warning" %}

    It is not recommended to exceed 10 hostnames per line on Windows. Split a long line into multiple lines if necessary.

    {% endinfo_block %}

    9. Click **File&nbsp;<span aria-label="and then">></span> Save**.
    10. Close the file.

5. Build and start the instance:

```bash
docker/sdk up
```

Depending on the hardware performance, the first project launch can take up to 20 minutes.


## Endpoints

To ensure that the installation is successful, make sure you can access the configured endpoints from the Deploy file. For more information about the Deploy file, see [Deploy file reference - 1.0](/docs/scos/dev/the-docker-sdk/{{site.version}}/deploy-file/deploy-file-reference-1.0.html).

{% info_block infoBox "RabbitMQ UI credentials" %}

To access RabbitMQ UI, use `spryker` as a username and `secret` as a password. You can adjust the credentials in `deploy.yml`.

{% endinfo_block %}

## Get the list of useful commands

To get the full and up-to-date list of commands, run `docker/sdk help`.

## Next steps

* [Troubleshooting](/docs/scos/dev/set-up-spryker-locally/troubleshooting-installation/troubleshooting-installation.html)
* [Configuring debugging in Docker](/docs/scos/dev/the-docker-sdk/{{site.version}}/configuring-debugging-in-docker.html)
* [Deploy File Reference - 1.0](/docs/scos/dev/the-docker-sdk/{{site.version}}/deploy-file/deploy-file-reference-1.0.html)
* [Configuring services](/docs/scos/dev/the-docker-sdk/{{site.version}}/configure-services.html)
* [Set up a self-signed SSL certificate](/docs/scos/dev/set-up-spryker-locally/configure-after-installing/set-up-a-self-signed-ssl-certificate.html)
