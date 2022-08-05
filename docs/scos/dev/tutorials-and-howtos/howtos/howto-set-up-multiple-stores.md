---
title: "HowTo: Set up multiple stores"
description: Learn how to set up multiple stores for your project.
last_updated: Nov 16, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/howto-set-up-multiple-stores
originalArticleId: 218ea4d5-de80-4aba-96fc-f67a9d13711c
redirect_from:
  - /2021080/docs/howto-set-up-multiple-stores
  - /2021080/docs/en/howto-set-up-multiple-stores
  - /docs/howto-set-up-multiple-stores
  - /docs/en/howto-set-up-multiple-stores
  - /v6/docs/howto-set-up-multiple-stores
  - /v6/docs/en/howto-set-up-multiple-stores
  - /docs/multiple-stores
  - /docs/en/multiple-stores
---

{% info_block warningBox "Multiple stores in cloud environments" %}

For instructions on setting up multiple stores in Spryker Cloud Commerce OS, see [Add and remove databases of stores](/docs/cloud/dev/spryker-cloud-commerce-os/multi-store-setups/add-and-remove-databases-of-stores.html).

{% endinfo_block %}

With the Spryker Commerce OS, you can create multiple stores per your business requirements for different scenarios. The multi-store setup is very versatile and customizable. For example, you can do the following:

* Build one store for multiple countries and languages or separate stores for each region.
* Make abstract products, discounts, and other logic and code shared between stores or create a dedicated setup for each of them.
* Define separate search preferences to create an entirely different set of rankings, rules, and settings per store. For example, a date format or a currency.
* Set up a default store.

## Multi-store setup infrastructure options

Multi-store setup 1: Database, search engine, and key-value storage are shared between stores.

![multi-store setup 1](https://spryker.s3.eu-central-1.amazonaws.com/docs/scos/dev/tutorials-and-howtos/howtos/how-to-set-up-multiple-stores.md/multi-store-setup-configuration-option-1.png)

Due to the resources being shared, the infrastructure costs are low. This setup is most suitable for B2C projects with low traffic and a small amount of data like products and prices.

Multi-store setup 2: Each store has a dedicated search engine and key-value storage while the database is shared.

![multi-store setup 2](https://spryker.s3.eu-central-1.amazonaws.com/docs/scos/dev/tutorials-and-howtos/howtos/how-to-set-up-multiple-stores.md/multi-store-setup-configuration-option-2.png)

This setup is most suitable for B2B projects with high traffic and a large amount of data.

Multi-store setup 3: Each store has a dedicated database, search engine, and key-value storage.

![multi-store setup 3](https://spryker.s3.eu-central-1.amazonaws.com/docs/scos/dev/tutorials-and-howtos/howtos/how-to-set-up-multiple-stores.md/multi-store-setup-configuration-option-3.png)

This setup is most suitable for the projects with the following requirements:

* Completely different business requirements per store, like business logic and features.
* Independent maintenance and development flow.
* Separated data management for entities like products, customers, and orders.
* On-demand setup of any type of environment per store, like test, staging, or production.

It’s the most expensive but flexible option in terms of per-store scaling and performance.

## Set up multiple stores

To set up multiple stores, follow the steps in the following sections:

### Configure code buckets

Code buckets provide an easy way to execute different business logic in runtime based on different HTTP or console command requests. To configure code buckets, see [Code buckets](/docs/scos/dev/architecture/code-buckets.html).

### Configure stores

1. Define the desired stores in `config/Shared/stores.php`. In the following example, DE and AT stores are defined:

<details><summary markdown='span'>config/Shared/stores.php</summary>

```php
<?php

$stores = [];

$stores['DE'] = [
    'contexts' => [
        '*' => [
            'timezone' => 'Europe/Berlin',
            'dateFormat' => [
                'short' => 'd/m/Y',
                'medium' => 'd. M Y',
                'rfc' => 'r',
                'datetime' => 'Y-m-d H:i:s',
            ],
        ],
        'yves' => [],
        'zed' => [
            'dateFormat' => [
                'short' => 'Y-m-d',
            ],
        ],
    ],
    // locales configuration
    'locales' => [
         'en' => 'en_US',
         'de' => 'de_DE',
    ],
    // country and currency configuration
    'countries' => ['DE'],
    'currencyIsoCode' => 'EUR',
    // Queue pool is the mechanism which sends messages to several queues.
    'queuePools' => [
        'synchronizationPool' => [
            'AT-connection',
            'DE-connection',
        ],
    ],
    'storesWithSharedPersistence' => ['AT'],
];

$stores['AT'] = [
    'contexts' => [
        '*' => [
            'timezone' => 'Europe/Vienna',
            'dateFormat' => [
                'short' => 'd/m/Y',
                'medium' => 'd. M Y',
                'rfc' => 'r',
                'datetime' => 'Y-m-d H:i:s',
            ],
        ],
        'yves' => [],
        'zed' => [
            'dateFormat' => [
                'short' => 'Y-m-d',
            ],
        ],
    ],
    'locales' => [
         'en' => 'en_US',
         'de' => 'de_AT',
    ],
    'countries' => ['AT'],
    'currencyIsoCode' => 'EUR',
];

return $stores;
```
</details>

2. Optional: Define store-specific configuration:
  1. For one or more stores you’ve defined in `config/Shared/stores.php`, define a separate store-specific configuration. For example, `config/Shared/config-default_docker_de.php` is the configuration file for the `DE` store in the docker environment.
  2. To apply the defined store-specific configuration, adjust the related deploy file in the `environment` section.

  In the following example, the `docker_de` environment name points to the `config/Shared/config-default_docker_de.php` store-specific configuration file. For more information about this deploy file parameter, see [environment](/docs/scos/dev/the-docker-sdk/{{site.version}}/deploy-file/deploy-file-reference-1.0.html#environment):

  ```yaml
  ....

  environment: docker_de

  image:
    tag:
  ```

3. Define the default store in `config/Shared/default_store.php`. In the following example, we define `DE` as the default store.

```php
<?php

return 'DE';
...
```

4. To import data for the stores you’ve added, adjust all the [import files and import configuration](/docs/scos/dev/data-import/{{site.version}}/data-importers-overview-and-implementation.html).

For example, define the import source for the `DE` store you’ve added:

```php
#2. Catalog Setup data import
...
- data_entity: product-price
  source: data/import/common/DE/product_price.csv
...   
```

5. Configure installation recipes

Add the new stores to the installation recipes in `config/install/*` as follows:

```yaml
...

stores:
    ...
    - {STORE_NAME}
...    
```

For example, to add the `AT` and `DE` stores, adjust an installation recipe as follows:

```yaml
...

stores:
    ...
    - DE
    - AT
...    
```

## Configure the deploy file

According to the desired infrastructure setup, configure the deploy file for the multi-store setup. In the following example, we configure the [multi-store setup 1](#multi-store-setup-infrastructure-options): database, search engine, and key-value storage are shared:

Deploy file configuration for the multi-store setup 1:

```yaml
......

regions:
    EU:
        services:
            mail:
                sender:
                    name: No-Reply
                    email: no-reply@example.com
            database:
                database: database-name
                username: database-username
                password: database-password
        stores:
            DE:
                services:
                    broker:
                        namespace: de_queue
                    key_value_store:
                        namespace: 1
                    search:
                        namespace: de_search
                    session:
                        namespace: 2
            AT:
                services:
                    broker:
                        namespace: at_queue
                    key_value_store:
                        namespace: 3
                    search:
                        namespace: at_search
                    session:
                        namespace: 4
....                        
```

The following configuration parameters are used in this example:

* The `regions` parameter defines one or more isolated instances of the Spryker applications that have only one persistent database to work with. The visibility of the project's stores is limited to operating only with the stores that belong to a region. Region refers to geographical terms like data centers, regions, and continents in the real world.
* The `stores` parameter defines the list of stores and store-specific settings for `services`.

For more information about deploy file configuration, see [Deploy file reference - 1.0](/docs/scos/dev/the-docker-sdk/{{site.version}}/deploy-file/deploy-file-reference-1.0.html).

## Define the store context

You can define stores by domains or by headers. We recommend defining stores by domains, which is supported by default.  

Defining stores by headers is not supported by default, but you can use the following workaround.

{% info_block infoBox %}

The workaround is only supported by the [multi-store store setup 1](#multi-store-setup-infrastructure-options) when all the resources are shared. With the other setup, you need to manage the infrastructure configuration on the application level.

**public/Glue/index.php**
```php
<?php

...
require_once APPLICATION_ROOT_DIR . '/vendor/autoload.php';

// Add this block
if (isset($_SERVER['HTTP_APPLICATION_STORE'])) {
    putenv('APPLICATION_STORE=' . $_SERVER['HTTP_APPLICATION_STORE']);
}

Environment::initialize();

...
```

To check if the workaround works, in the browser console, run the following:
```php
fetch("http://{domain-name}/catalog-search", {
  "headers": {
    "upgrade-insecure-requests": "1",
    "application-store": "MY_STORE"
  },
  "referrerPolicy": "strict-origin-when-cross-origin",
  "body": null,
  "method": "GET",
  "mode": "cors",
  "credentials": "omit"
}).then(r => console.log(r.text()));
```

{% endinfo_block %}

You’ve successfully added the stores and can access them according to how you’ve defined their context.
