

{% info_block errorBox %}

This feature integration guide expects the basic feature to be in place.
The current feature integration guide adds the Cart Notes Backend API functionality.

{% endinfo_block %}

## Prerequisites

To start feature integration, integrate the required feature:

| NAME             | VERSION          | INTEGRATE GUIDE                                                                                                                              |
|------------------|------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Order Management | {{page.version}} | [Order Management feature integration](/docs/scos/dev/feature-integration-guides/{{page.version}}/install-the-order-management-feature.html) |

## 1) Install the required modules using Composer

```bash
composer require spryker-feature/cart-notes:"{{page.version}}" --update-with-dependencies
```

Ensure that the following modules have been installed:

| MODULE                | EXPECTED DIRECTORY                      |
|-----------------------|-----------------------------------------|
| CartNotesBackendApi   | vendor/spryker/cart-notes-backend-api   |

## 2) Set up transfer objects

Generate transfers:

```bash
console transfer:generate
```

{% info_block warningBox "Verification" %}

Make sure that the following changes have been triggered in transfer objects:

| TRANSFER                            | TYPE     | EVENT   | PATH                                                             |
|-------------------------------------|----------|---------|------------------------------------------------------------------|
| OrdersBackendApiAttributes.cartNote | property | created | src/Generated/Shared/Transfer/OrdersBackendApiAttributesTransfer |

{% endinfo_block %}

## 3) Set up behavior

1. Enable the following behaviors by registering the plugins:

| PLUGIN                                         | SPECIFICATION                                                          | PREREQUISITES | NAMESPACE                                                     |
|------------------------------------------------|------------------------------------------------------------------------|---------------|---------------------------------------------------------------|
| CartNoteOrdersBackendApiAttributesMapperPlugin | Expands `ApiOrdersAttributes.cartNote` with `Order.cartNote` property. |               | Spryker\Glue\CartNotesBackendApi\Plugin\SalesOrdersBackendApi |

**src/Pyz/Glue/SalesOrdersBackendApi/SalesOrdersBackendApiDependencyProvider.php**

```php
<?php

namespace Pyz\Glue\SalesOrdersBackendApi;

use Spryker\Glue\CartNotesBackendApi\Plugin\SalesOrdersBackendApi\CartNoteOrdersBackendApiAttributesMapperPlugin;
use Spryker\Glue\SalesOrdersBackendApi\SalesOrdersBackendApiDependencyProvider as SprykerSalesOrdersBackendApiDependencyProvider;

class SalesOrdersBackendApiDependencyProvider extends SprykerSalesOrdersBackendApiDependencyProvider
{
    /**
     * @return list<\Spryker\Glue\SalesOrdersBackendApiExtension\Dependency\Plugin\OrdersBackendApiAttributesMapperPluginInterface>
     */
    protected function getOrdersBackendApiAttributesMapperPlugins(): array
    {
        return [
            new CartNoteOrdersBackendApiAttributesMapperPlugin(),
        ];
    }
}
```

{% info_block warningBox "Verification" %}

Make sure that `sales-orders` resources from `SalesOrdersBackendApiResource::getOrderResourceCollection()` results contain cart note data: `OrderResourceCollectionTransfer.orderResources.attributes.cartNote` are set for the orders that have cart notes.

{% endinfo_block %}