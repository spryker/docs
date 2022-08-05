---
title: Developer getting started guide
description: This is a step-by-step checklist that you can follow through all the stages of working with Spryker.
last_updated: July 11, 2022
template: concept-topic-template
originalLink: https://documentation.spryker.com/2021080/docs/dev-getting-started
originalArticleId: 79b50d48-6f09-45b0-9e4a-f372e274d462
redirect_from:
  - /2021080/docs/dev-getting-started
  - /2021080/docs/en/dev-getting-started
  - /docs/dev-getting-started
  - /docs/en/dev-getting-started
  - /v6/docs/dev-getting-started
  - /v6/docs/en/dev-getting-started
  - /v5/docs/dev-getting-started
  - /v5/docs/en/dev-getting-started
  - /v4/docs/dev-getting-started
  - /v4/docs/en/dev-getting-started
  - /v3/docs/dev-getting-started
  - /v3/docs/en/dev-getting-started
  - /v2/docs/dev-getting-started
  - /v2/docs/en/dev-getting-started
  - /v1/docs/dev-getting-started
  - /v1/docs/en/dev-getting-started
  - /2021080/docs/about-the-development-guide
  - /2021080/docs/en/about-the-development-guide
  - /docs/about-the-development-guide
  - /docs/en/about-the-development-guide
  - /v6/docs/about-the-development-guide
  - /v6/docs/en/about-the-development-guide
  - /v5/docs/about-the-development-guide
  - /v5/docs/en/about-the-development-guide
  - /v4/docs/about-the-development-guide
  - /v4/docs/en/about-the-development-guide
  - /v3/docs/about-the-development-guide
  - /v3/docs/en/about-the-development-guide
  - /v2/docs/about-the-development-guide
  - /v2/docs/en/about-the-development-guide
  - /v1/docs/about-the-development-guide
  - /v1/docs/en/about-the-development-guide
  - /v4/docs/installation-guide-b2c
  - /v4/docs/en/installation-guide-b2c
  - /v4/docs/installation-guide-b2b
  - /v4/docs/en/installation-guide-b2b  -
  - /2021080/docs/installation-guide-b2c
  - /2021080/docs/en/installation-guide-b2c
  - /docs/installation-guide-b2c
  - /docs/en/installation-guide-b2c
---

This document guides you into getting started with the Spryker Commerce OS. It has been structured as a step-by-step checklist to help get you through all of the stages involved in working with Spryker. After following these instructions, if you still have any questions, you can access our [Spryker Community Slack group](https://sprykercommunity.slack.com/join/shared_invite/zt-gdakzwk3-~B_gJXbUxMdzkBwTQVjNgg#/).

## 1. Install Spryker

For the starting point of any project, it is good to start from one of the Spryker Demo Shops that are available. They act as a typical Spryker installation and help to establish different types of the Spryker Commerce OS. A Demo Shop includes different sets of components that have been selected for a different type of business or project. Each of these options is fully functional and can be used for both demonstrative purposes as well as working as a boilerplate for your new project. Though each shop comes with its own pre-selected components, Spryker also offers hundreds of additional modules which can be chosen later.

You can choose from the following options:

* [B2B Demo Shop](/docs/scos/user/intro-to-spryker//b2b-suite.html): A boilerplate for B2B commerce projects.
* [B2C Demo Shop](/docs/scos/user/intro-to-spryker/b2c-suite.html): A starting point for B2C implementations.

Both Demo Shops can also be expanded with separate [features](/docs/scos/user/features/{{site.version}}/features.html) and modules.

### Install Spryker with Docker

When installing Spryker, we recommend starting with a Docker SDK environment. It features a lightweight environment that is closer to production implementation. This option includes Docker and related tools to build and run containers that match your requirements. 

To start developing your Spryker in Docker, see [Installing Spryker with Docker](/docs/scos/dev/setup/installing-spryker-with-docker/installing-spryker-with-docker.html). Spryker can be run on MacOS, Linux, and Windows with WSL1 or WSL2.

* Make sure you have all of the necessary [prerequisites before installing docker](/docs/scos/dev/setup/installing-spryker-with-docker/installing-spryker-with-docker.html#prerequisites).
* Once you have the necessary prerequisites set up, you can then [choose your installation mode with your OS](/docs/scos/dev/setup/installing-spryker-with-docker/installing-spryker-with-docker.html#installation). You can install docker in modes for Development, Demo, or add it to an existing project.

#### The deploy file

When working with a local environment, you should use the [deploy.dev.yml](/docs/scos/dev/the-docker-sdk/202108.0/deploy-file/deploy-file.html) file.

In the default deploy file, change the following attributes:

* Namespace: We recommend specifying the name for your project, as this helps to avoid issues when you have two or more projects with the same names
* Regions
* Stores
* Domains for the local environment
* Domains for the services (RabbitMQ, Jenkins): Optional, but this can help to keep all project links together

#### Vagrant clean-up

When you use Docker and not the Development Virtual Machine (also called DevVM), you do not need the DevVM’s configuration files. Therefore, you can remove the following files:

* `config/install/development.yml`
* `config_default-development_*.php`

### Install Spryker with the Development Virtual Machine

The Spryker Commerce OS offers a Virtual Machine, which includes all of the prerequisites needed to run Spryker. It provides a full-featured development environment, which helps you customize Spryker based on your project’s requirements. The Development Virtual Machine (DevVM) is based on VirtualBox and Vagrant and can be used to install Spryker on any operating system.

{% info_block warningBox "DevVM is deprecated" %}

We will soon deprecate the DevVM and stop supporting it. Therefore, we highly recommend [installing Spryker with Docker](#install-spryker-with-docker).

{% endinfo_block %}

We offer a number of installation guides that may suit your needs:

| OPERATION SYSTEMS | B2B SHOP OR B2C SHOP |
| --- | --- |
| DevVM on Linux / Mac OS | [B2B or B2C Demo Shop installation: Mac OS or Linux, with Development Virtual Machine](/docs/scos/dev/setup/installing-spryker-with-development-virtual-machine/installing-spryker-with-devvm-on-macos-and-linux.html) |
| DevVM on Windows | [B2B or B2C Demo Shop installation: Windows, with Development Virtual Machine](/docs/scos/dev/setup/installing-spryker-without-development-virtual-machine-or-docker.html) |

### Independent installation

Alternatively, you can install Spryker without the Docker images. See [Installing Spryker without Docker](/docs/scos/dev/setup/installing-spryker-without-docker.html) for details.

{% info_block warningBox %}

Following your installation, make sure to check out [Post-Installation steps and additional info](/docs/scos/dev/setup/installing-spryker-with-development-virtual-machine/configuring-spryker-with-devvm/configuring-spryker-after-installing-with-devvm.html) for tips on fine-tuning Spryker.

{% endinfo_block %}

### Adjust the `readme.md` file

Once your project has been installed, you need to adjust the `readme.md` file in the following ways:

* Update the project installation description.
* Update the repository link.
* Remove any unused information, such as Vagrant installation instructions if a DevVM was not used.
* Consider moving the production information further done in the file so that new developers can more readily understand how to use the project.

## 2. Manage modules

Once the installation of your new project has been completed, you may start to manage the modules you want to use. A module within Spryker is a single-function unit that has well-defined dependencies and can be updated independently.

{% info_block infoBox %}

To better define your strategy when implementing Spryker updates, learn about our [module and feature release process](/docs/scos/user/intro-to-spryker/spryker-release-process.html).

{% endinfo_block %}

When installing and managing module dependencies, we use [Composer](/docs/scos/dev/setup/managing-scos-dependencies-with-composer.html). Depending on what you want to do, you can run one of the following Composer commands:

* To install the dependencies you listed in the `composer.json` file of the project: `composer install`.
* To update all the modules for your project: `composer update "spryker/*"`.

{% info_block infoBox %}

We recommend running this command weekly to ensure you have the latest fixes. We also recommend [subscribing to our release notes newsletter](https://now.spryker.com/release-notes) to stay up-to-date with the improvements.

{% endinfo_block %}

* To update a particular module: `composer update "spryker/module-name"`. 

{% info_block infoBox %}

You can easily keep track of new module versions using the [composer-versions-check](https://github.com/Soullivaneuh/composer-versions-check) addon for your local Composer tool.

{% endinfo_block %}

* To add a new module to your project: `composer require "spryker/module-name"`.

To learn about the module versioning approach in Spryker, see [Semantic Versioning: Major vs. Minor vs. Patch Release](/docs/scos/dev/architecture/module-api/semantic-versioning-major-vs.-minor-vs.-patch-release.html).

## 3. Configure the environment

The next step to take once installation has finished and modules set up, you need to configure and customize your Spryker Commerce OS. For this, you can do the following:

1. Define how to manage the settings in the configuration files with [Configuration management](/docs/scos/dev/back-end-development/data-manipulation/configuration-management.html).
2. Configure your environment:
    * [Database](/docs/scos/dev/setup/installing-spryker-with-development-virtual-machine/configuring-spryker-with-devvm/configuring-database-servers.html)
    * [Redis](/docs/scos/dev/setup/redis-configuration.html)
    <!---*   [ElasticSearch](/docs/scos/dev/back-end-development/data-manipulation/data-interaction/search/configuring-elasticsearch.html)-->
    * [Queue](/docs/scos/dev/back-end-development/data-manipulation/queue/queue.html)
3. [Configure stores](/docs/scos/dev/tutorials-and-howtos/howtos/howto-set-up-multiple-stores.html#configure-stores) depending on your need for one or multiple stores in your online shop.
4. [Schedule tasks](/docs/scos/dev/back-end-development/cronjobs/cronjobs.html) (Cron jobs).
<!---4. Move to the maintenance mode-->

### Store clean-up

This step depends on the store setup you came up with during your configuring. For example, if you choose to start with just one store, you should clean up the remaining stores in the following files:

* `config/install/*`
* `data/import/*`
* `deploy.dev.yml`
* `config_default.php`
* `src/SprykerConfig/CodeBucketConfig.php`

### Modules clean-up

* Analyze modules that you have in the desired Demoshop.
* Analyze modules that you need to have.
* Remove unnecessary modules (to do that, you can use the migration guide backward).

### Data import clean-up

Located in the `data/import` folder, you may find additional files related to these other stores. As with cleaning up stores, you must define the stores you intend to use and remove unused files of the rest. 

{% info_block infoBox "Info" %}

Keep in mind that you must also change the default config in `DataImportConfig::getDefaultYamlConfigPath()`.

{% endinfo_block %}

For those stores that you wish to allow, don’t forget to edit `CodeBucketConfig::getCodeBuckets()`.

## 4. Configure CI

Continuous Integration (CI) is a development practice where each part of the code can be verified by an automated build and automated tests. This allows for good code quality and that each new feature does not break the existing functionality. The following documents will help you to enable CI in different repositories:
* [Deployment pipelines](/docs/cloud/dev/spryker-cloud-commerce-os/configure-deployment-pipelines/configuring-azure-pipelines.html)
* [Customizing deployment pipelines](/docs/cloud/dev/spryker-cloud-commerce-os/configure-deployment-pipelines/configuring-bitbucket-pipelines.html)
* [GitHub Actions](/docs/cloud/dev/spryker-cloud-commerce-os/configure-deployment-pipelines/configuring-github-actions.html)
* [Configuring GitLab pipelines](/docs/cloud/dev/spryker-cloud-commerce-os/configure-deployment-pipelines/configuring-gitlab-pipelines.html)
* [Azure Pipelines](/docs/cloud/dev/spryker-cloud-commerce-os/configure-deployment-pipelines/configuring-azure-pipelines.html)
* [Configuring Bitbucket Pipelines ](/docs/cloud/dev/spryker-cloud-commerce-os/configure-deployment-pipelines/configuring-bitbucket-pipelines.html)

## 5. Configure checkers

To keep your code clean, we recommend using code checkers. To keep your code clean, we recommend using the code checkers.

### Code Sniffer

Before running any code sniffer, we recommend that you update it to its latest version. There are often changes that introduce new checks which help to increase the quality of code. When updating, be sure to keep in mind that you will also need to make changes to the `composer.json` file.

```bash
composer update spryker/code-sniffer slevomat/coding-standard --with-dependencies
```

At the project level, you may choose to use your own rules or to exclude rules enabled in Spryker by default.

* To activate a new rule, check out the full list of rules at [Slevomat Coding Standard](https://github.com/slevomat/coding-standard).
* To disable a rule, you can use configuration. The following example excludes a rule that makes annotation for constructor and method required:

```yaml
<rule ref="vendor/spryker/code-sniffer/Spryker/ruleset.xml">
        <exclude name="Spryker.Commenting.DocBlock"/>
</rule>
```
### PHPStan

When using PHPStan, we recommend version 1.2.* or later. These versions help you avoid memory and other issues.

This can be toggled at the project level by enabling rule level 6:

```yaml
vendor/bin/phpstan analyze -l 6 -c phpstan.neon src/
```

## 6. Configure PhpStorm

If you wish to speed up your work, we recommend configuring PhpStorm.

### Plugins

Make sure to configure the following plugins:

### Speed up indexation
At the beginning of the project, you need to reset your project quite often. PhpStorm indexing is annoying and takes too much of the resources. To avoid this, you can disable cache indexing.

To disable cache indexing, in the PhpStorm, right-click the folder and select **Mark Directory As&nbsp;<span aria-label="and then">></span> Excluded**.

It is safe to disable cache indexing for the following files:

* `data/cache `
* `data/tmp`
* `public/(Yves/Zed/Marketlace)/assets`

## 7. Configure debugging

Before you start developing, you should set up and get to know your debugging environment. To learn how to configure debugging, see one of the following: 

* [Configuring debugging in Docker](/docs/scos/dev/the-docker-sdk/{{site.version}}/configuring-debugging-in-docker.html)
* [Configuring debugging in DevVM](/docs/scos/dev/setup/installing-spryker-with-development-virtual-machine/configuring-debugging-in-devvm/configuring-debugging-in-devvm.html)

{% info_block infoBox %}

When in a production environment, Zed must be configured to use a VPN, basic access authentication, or an IP allowlist.

{% endinfo_block %}

## 8. Familiarize yourself with the Spryker architecture

As a developer, the Spryker structure is the first thing you need to know to extend the core functionality. To familiarize yourself with the Spryker architecture, different parts of the Client, Shared, Zed, and Yves folders, and their different layers, see the following documents:

* [Conceptual overview](/docs/scos/dev/architecture/conceptual-overview.html): to learn about application layers and code structure.
* [Modules and layers](/docs/scos/dev/architecture/modules-and-layers.html): to learn about layers and how various functionality is encapsulated in modules.
* [Programming concepts](/docs/scos/dev/architecture/programming-concepts.html): to learn about the Spryker building blocks contained in the application layers.
* [Technology stack](/docs/scos/dev/architecture/technology-stack.html): to learn about the technologies we use.

<!---* Introduction to navigating the folder structure, main concepts and namespacing.
* The project directory
* The OS directories-->

<!---## Step 5: The Development Virtual Machine

Get to know the parts of the Spryker Development Virtual Machine with which we ship the Spryker Commerce OS so that you have a pre-configured and ready-to-go stack.

* What is the Spryker DevVM (Development Virtual Machine) and why do we need it?
* Main Structure
* Technology Stack: Linux distribution, PHP, Postgres, MySQL, ES, Redis, Queue, Jenkins-->
