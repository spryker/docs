

This document describes how to install the Zed API Merchant Relationships.

## Install feature core

Follow the steps below to install the Zed API for Merchant Relationships feature core.

### Prerequisites

To start feature integration, integrate the required features and Glue APIs:

| NAME   | VERSION    | INSTALLATION GUIDE   |
|-------------------------|-------------------|---------------------------|
| Zed API                     | {{page.version}}  | [Zed API feature integration](/docs/scos/dev/feature-integration-guides/{{page.version}}/zed-api-feature-integration.html)                                          |
| Merchants and Merchant Relations | {{page.version}}  | [Merchants and Merchant Relations feature integration](/docs/pbc/all/merchant-management/{{page.version}}/base-shop/install-and-upgrade/install-the-merchants-and-merchant-relations-feature.html) |
| Spryker Core                    | {{page.version}}  | [Install the Spryker Core feature](/docs/scos/dev/feature-integration-guides/{{page.version}}/spryker-core-feature-integration.html)                                        |

### 1) Install the required modules using Composer

Install the required modules:

```bash
composer require spryker/merchant-relationship-api:"^0.1.0" --update-with-dependencies
```

{% info_block warningBox "Verification" %}

Make sure that the following modules have been installed:

| MODULE                   | EXPECTED DIRECTORY                       |
|--------------------------|------------------------------------------|
| MerchantRelationshipApi  | vendor/spryker/merchant-relationship-api |

{% endinfo_block %}

### 2) Set up transfer objects

Generate transfers:

```bash
console transfer:generate
```

{% info_block warningBox "Verification" %}

Make sure that the following changes have been triggered in transfer objects:

| TRANSFER                            | TYPE  | EVENT   | PATH                                                                          |
|-------------------------------------|-------|---------|-------------------------------------------------------------------------------|
| MerchantRelationshipApi             | class | created | src/Generated/Shared/Transfer/MerchantRelationshipApiTransfer.php             |
| MerchantRelationshipBusinessUnitApi | class | created | src/Generated/Shared/Transfer/MerchantRelationshipBusinessUnitApiTransfer.php |
| MerchantRelationshipProductListApi  | class | created | src/Generated/Shared/Transfer/MerchantRelationshipProductListApiTransfer.php  |

{% endinfo_block %}

### 3) Set up behavior

Enable the following behaviors by registering the plugins:

| PLUGIN      | SPECIFICATION        | PREREQUISITES | NAMESPACE      |
|-----------------------|---------------------|---------------|--------------------|
| MerchantRelationshipApiResourcePlugin   | Configures CRUD actions for `merchant-relationships` resource. |               | Spryker\Zed\MerchantRelationshipApi\Communication\Plugin\Api  |
| MerchantRelationshipApiValidatorPlugin  | Validates if all required fields are present in request data.  |               | Spryker\Zed\MerchantRelationshipApi\Communication\Plugin\Api  |

```php
<?php

namespace Pyz\Zed\Api;

use Spryker\Zed\Api\ApiDependencyProvider as SprykerApiDependencyProvider;
use Spryker\Zed\MerchantRelationshipApi\Communication\Plugin\Api\MerchantRelationshipApiResourcePlugin;
use Spryker\Zed\MerchantRelationshipApi\Communication\Plugin\Api\MerchantRelationshipApiValidatorPlugin;

class ApiDependencyProvider extends SprykerApiDependencyProvider
{
    /**
     * @return array<\Spryker\Zed\Api\Dependency\Plugin\ApiResourcePluginInterface>
     */
    protected function getApiResourcePluginCollection(): array
    {
        return [
            new MerchantRelationshipApiResourcePlugin(),
        ];
    }

    /**
     * @return array<\Spryker\Zed\ApiExtension\Dependency\Plugin\ApiValidatorPluginInterface>
     */
    protected function getApiValidatorPluginCollection(): array
    {
        return [
            new MerchantRelationshipApiValidatorPlugin(),
        ];
    }
}

```

{% info_block warningBox "Verification" %}

Make sure that the `https://zed-api.mysprykershop.com/api/rest/merchant-relationships` endpoint is available.

Make sure that data is validated by providing an invalid merchant reference in a request body.

Request body example:

```json
{
    "data": {
        "merchantReference": "MER000006",
        "idCompany": "11",
        "idBusinessUnitOwner": "30",
        "assignedBusinessUnits": [
            {
                "idCompanyBusinessUnit": 24
            }
        ],
        "assignedProductLists": [
            {
                "idProductList": 14
            },
            {
                "idProductList": 4
            }
        ]
    }
}
```

Response example:

```json
{
  "code": 200,
  "message": null,
  "data": {
    "idMerchantRelationship": 19,
    "idBusinessUnitOwner": 30,
    "businessUnitOwnerName": "IT no ASUS",
    "idCompany": 11,
    "companyName": "Restricted 1",
    "merchantName": "Restrictions Merchant",
    "merchantReference": "MER000006",
    "assignedBusinessUnits": [
      {
        "name": "IT no tablets",
        "idCompanyBusinessUnit": 24
      }
    ],
    "assignedProductLists": [
      {
        "idProductList": 14,
        "name": "All computers"
      },
      {
        "idProductList": 4,
        "name": "No ASUS"
      }
    ]
  },
  "links": [],
  "meta": []
}
```

{% endinfo_block %}
