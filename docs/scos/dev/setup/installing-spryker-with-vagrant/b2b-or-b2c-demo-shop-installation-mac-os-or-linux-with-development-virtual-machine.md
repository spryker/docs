---
title: B2B or B2C Demo Shop installation- Mac OS or Linux, with Development Virtual Machine
description: This article provides step-by-step instructions on the B2B or B2C Demo Shop installation on Mac OS or Linux with Development Virtual Machine.
last_updated: Oct 18, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/b2b-b2c-demo-shop-installation-mac-os-or-linux-with-devvm
originalArticleId: 1d644ef6-acab-4d55-afa8-24628043bae7
redirect_from:
  - /2021080/docs/b2b-b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /2021080/docs/en/b2b-b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /docs/b2b-b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /docs/en/b2b-b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /v6/docs/b2b-b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /v6/docs/en/b2b-b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /v5/docs/b2b-b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /v5/docs/en/b2b-b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /v4/docs/installation-guide-b2b
  - /v4/docs/en/installation-guide-b2b
  - /v4/docs/b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /v4/docs/en/b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /v3/docs/installation-guide-b2b
  - /v3/docs/en/installation-guide-b2b
  - /v3/docs/b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /v3/docs/en/b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /v2/docs/installation-guide-b2b
  - /v2/docs/en/installation-guide-b2b
  - /v2/docs/b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /v2/docs/en/b2c-demo-shop-installation-mac-os-or-linux-with-devvm
  - /v1/docs/installation-guide-b2b
  - /v1/docs/en/installation-guide-b2b
  - /v1/docs/installation-guide-b2c
  - /v1/docs/en/installation-guide-b2c
---

To install the Demo Shop for [B2B](/docs/scos/user/intro-to-spryker/b2b-suite.html) or [B2C](/docs/scos/user/intro-to-spryker/b2c-suite.html) implementations on Mac OS or Linux with Development Virtual Machine, follow the steps below.

### 1. Install prerequisites

To set up your environment, install the following prerequisites:

* [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [VirtualBox 5.2.2+](https://www.virtualbox.org/wiki/Downloads)
* [Vagrant 2.0.0+](https://www.vagrantup.com/downloads.html)
* *vagrant-vbguest* and *vagrant-hostmanager* plugins:

```bash
vagrant plugin install vagrant-vbguest
vagrant plugin install vagrant-hostmanager
```

### 2. Install Spryker Virtual Machine

Run the following commands in your favorite shell (e.g. `Bash`):

1. **Create the folder in which you want the source code to be placed:**

```bash
mkdir devvm
cd devvm						
```

2. **Initialize the Vagrant environment**:

```bash
vagrant init devv410 https://u220427-sub1:PpiiHzuF2OIUzmcH@u220427-sub1.your-storagebox.de/devvm_v4.1.0.box
```
{% info_block warningBox %}

For _Spryker Core_ version **201907.0** or prior, you need to use an older version of the development machine:
```bash
vagrant init devvm2.3.1 https://github.com/spryker/devvm/releases/download/v2.3.1/spryker-devvm.box
```

{% endinfo_block %}

3. **Update the Vagrantfile**:

Add hostmanager plugin configuration:

```bash
mv Vagrantfile Vagrantfile.bak
awk '/^end/{print "  config.hostmanager.enabled = true\n  config.hostmanager.manage_host = true"}1' Vagrantfile.bak > Vagrantfile
```

4. **Build and start the virtual machine**:
* For a B2B Demo Shop:

```bash
VM_PROJECT=b2b-demo-shop SPRYKER_REPOSITORY="https://github.com/spryker-shop/b2b-demo-shop.git" vagrant up
```

* For a B2C Demo Shop:
```bash
VM_PROJECT=b2c-demo-shop SPRYKER_REPOSITORY="https://github.com/spryker-shop/b2c-demo-shop.git" vagrant up
```

When the VM is built and running, your local copy of the repository will be placed in the `project` subfolder of the folder where the VM is located (e.g. `~/devvm/project`). The subfolder will be mounted inside the VM to `/data/shop/development/current`.

### 3. Install the shop

1. **Log into the VM:**

```bash
vagrant ssh
```

2. **Run the installation commands:**

```bash
composer install
vendor/bin/install
```

{% info_block warningBox %}

If you are using a devvm version lower than 2.2.0, run the `ulimit -n 65535` command first.

{% endinfo_block %}

Executing these steps will install all required dependencies, and run the installation process. Also, this will install the demo data and export it to `Redis` and `Elasticsearch`.

When the installation process is complete, Spryker Commerce OS is ready to use. It can be accessed via the following links:

**B2B Demo Shop:**
* `http://de.b2b-demo-shop.local` - front-end (Storefront);
* `http://zed.de.b2b-demo-shop.local` - backend (the Back Office).
* `http://glue.de.b2b-demo-shop.local` - REST API (Glue).

**B2C Demo Shop:**
* `http://de.b2c-demo-shop.local/` - front-end (Storefront);
* `http://zed.de.b2c-demo-shop.local` - backend (the Back Office).
* `http://glue.de.b2c-demo-shop.local` - REST API (Glue).

Credentials to access the administrator interface: user `admin@spryker.com` and password `change123`.

## Next steps:
* [Troubleshooting installation issues](/docs/scos/dev/troubleshooting/troubleshooting-spryker-in-vagrant-issues/troubleshooting-spryker-in-vagrant-installation-issues.html)
