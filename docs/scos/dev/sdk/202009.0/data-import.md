---
title: Data import
description: Easily import your business logic and data, such as Product Information, Customer Base, Categories and many more into the Spryker Commerce OS.
template: concept-topic-template
originalLink: https://documentation.spryker.com/v6/docs/importer
originalArticleId: a1d197eb-94ef-424f-a26a-a9f598ee51db
redirect_from:
  - /v6/docs/importer
  - /v6/docs/en/importer
related:
  - title: About Demo Shop Data Import
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/importing-demo-shop-data.html
  - title: Execution Order of Data Importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
  - title: About Data Import Categories
    link: docs/scos/dev/data-import/page.version/data-import-categories/about-data-import-categories.html
  - title: Importing Data with the Queue Data Importer
    link: docs/scos/dev/data-import/page.version/importing-data-with-the-queue-data-importer.html
---

Easily import your business logic and data, such as Product Information, Customer Base, Categories, and many more into the Spryker Commerce OS.

The* Data Import* feature allows you to configure what you need to import. You don't need to import all data that is available in Spryker OS out of the box. Instead, you can define what data you want to import for your project using a YAML configuration file. See [Importing data with a configuration file](/docs/scos/dev/data-import/{{page.version}}/importing-data-with-a-configuration-file.html) for details on how you can do that.
{% info_block infoBox "Data import help" %}

To help you build your import files, define the correct order of the data importers to run, there is the [Data import documentation](/docs/scos/dev/data-import/{{page.version}}/data-import-categories/about-data-import-categories.html) for your reference. Consult it whenever you need to import data into your project.

{% endinfo_block %}

The main benefits of the Data Import feature are:

* Allows for flexibility to set up initial data and update new information using configuration (YAML) file as a parameter of the `data:import console` command.
* Presupposes batch data files import, allowing to change sequence order, without changing the project’s source code.
* Reduces new projects time-to-market due to a high agility to run frequent data updates.
* Increases business people autonomy (online store manager, purchasing agent, warehouse manager, analyst, etc.), as the data changes are handled flexibly.

**What's next?**

* For an overview and implementation details of the Spryker data importers, see [Data importers overview and implementation](/docs/scos/dev/data-import/{{page.version}}/data-importers-overview-and-implementation.html).
* To create your own data importer, see [Creating a data importer](/docs/scos/dev/data-import/{{page.version}}/creating-a-data-importer.html).
* To import the Demo Shop data, see [Importing Demo Shop data](/docs/scos/dev/data-import/{{page.version}}/demo-shop-data-import/importing-demo-shop-data.html) and[ About data import categories](/docs/scos/dev/data-import/{{page.version}}/data-import-categories/about-data-import-categories.html).
* To import data with a YAML configuration file, see [Importing data with a configuration file](/docs/scos/dev/data-import/{{page.version}}/importing-data-with-a-configuration-file.html).


