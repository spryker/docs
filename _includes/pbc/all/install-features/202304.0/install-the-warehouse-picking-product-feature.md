


This document describes how to integrate the Warehouse picking + [Product](/docs/pbc/all/product-information-management/{{site.version}}/feature-overviews/product-feature-overview/product-feature-overview.html) feature into a Spryker project.

## Install feature core

Follow the steps below to install the Warehouse Picking + Product feature core.

### Prerequisites

To start feature integration, integrate the required features:

| NAME              | VERSION          | INTEGRATION GUIDE                                                                                                                                                 |
|-------------------|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Warehouse Picking | {{site.version}} | [Warehouse Picking feature integration](/docs/scos/dev/feature-integration-guides/{{site.version}}/install-the-warehouse-picking-feature.html)                    |
| Product           | {{site.version}} | [Product feature integration](docs/pbc/all/product-information-management/{{site.version}}/install-and-upgrade/install-features/install-the-product-feature.html) |


## 1) Install the required modules using Composer

```bash
composer require spryker/picking-lists-products-backend-resource-relationship:"^0.1.0" --update-with-dependencies
```

{% info_block warningBox "Verification" %}

Make sure that the following module has been installed:

| MODULE                                          | EXPECTED DIRECTORY                                                  |
|-------------------------------------------------|---------------------------------------------------------------------|
| PickingListsProductsBackendResourceRelationship | vendor/spryker/picking-lists-products-backend-resource-relationship |

{% endinfo_block %}

### 2) Set up behavior

Enable the following plugins.

| PLUGIN                                                              | SPECIFICATION                                                                           | PREREQUISITES | NAMESPACE                                                                                                                   |
|---------------------------------------------------------------------|-----------------------------------------------------------------------------------------|---------------|-----------------------------------------------------------------------------------------------------------------------------|
| ConcreteProductsByPickingListItemsBackendResourceRelationshipPlugin | Adds `concrete-products` resources as a relationship to `picking-list-items` resources. |               | Spryker\Glue\PickingListsProductsBackendResourceRelationship\Plugin\GlueBackendApiApplicationGlueJsonApiConventionConnector |


**src/Pyz/Glue/GlueBackendApiApplicationGlueJsonApiConventionConnector/GlueBackendApiApplicationGlueJsonApiConventionConnectorDependencyProvider.php**

```php
<?php

namespace Pyz\Glue\GlueBackendApiApplicationGlueJsonApiConventionConnector;

use Spryker\Glue\GlueBackendApiApplicationGlueJsonApiConventionConnector\GlueBackendApiApplicationGlueJsonApiConventionConnectorDependencyProvider as SprykerGlueBackendApiApplicationGlueJsonApiConventionConnectorDependencyProvider;
use Spryker\Glue\GlueJsonApiConventionExtension\Dependency\Plugin\ResourceRelationshipCollectionInterface;
use Spryker\Glue\PickingListsBackendApi\PickingListsBackendApiConfig;
use Spryker\Glue\PickingListsProductsBackendResourceRelationship\Plugin\GlueJsonApiConvention\ConcreteProductsByPickingListItemsBackendResourceRelationshipPlugin;

class GlueBackendApiApplicationGlueJsonApiConventionConnectorDependencyProvider extends SprykerGlueBackendApiApplicationGlueJsonApiConventionConnectorDependencyProvider
{
    /**
     * @param \Spryker\Glue\GlueJsonApiConventionExtension\Dependency\Plugin\ResourceRelationshipCollectionInterface $resourceRelationshipCollection
     *
     * @return \Spryker\Glue\GlueJsonApiConventionExtension\Dependency\Plugin\ResourceRelationshipCollectionInterface
     */
    protected function getResourceRelationshipPlugins(
        ResourceRelationshipCollectionInterface $resourceRelationshipCollection,
    ): ResourceRelationshipCollectionInterface {
        $resourceRelationshipCollection->addRelationship(
            PickingListsBackendApiConfig::RESOURCE_PICKING_LIST_ITEMS,
            new ConcreteProductsByPickingListItemsBackendResourceRelationshipPlugin(),
        );

        return $resourceRelationshipCollection;
    }
}


```

{% info_block warningBox "Verification" %}

Make sure you have a `concrete-products` resource as a relationship to `picking-list-items` when you do a request.

`GET https://glue-backend.mysprykershop.com/picking-lists/{% raw %}{{{% endraw %}picking-list-uuid{% raw %}}{{% endraw %}?include=picking-list-items,concrete-products`
<details>
  <summary markdown='span'>Response body example</summary>
```json
{
    "data": {
        "id": "14baa0f3-e6e7-5aa8-bc6c-c02ec39ca77b",
        "type": "picking-lists",
        "attributes": {
            "status": "ready-for-picking",
            "createdAt": "2023-03-23 15:47:07.000000",
            "updatedAt": "2023-03-23 15:49:57.000000"
        },
        "relationships": {
            "picking-list-items": {
                "data": [
                    {
                        "id": "65bb3aec-0a45-5ec6-9b12-bbca6551d87f",
                        "type": "picking-list-items"
                    }
                ]
            }
        },
        "links": {
            "self": "https://glue-backend.mysprykershop.com/picking-lists/14baa0f3-e6e7-5aa8-bc6c-c02ec39ca77b?include=picking-list-items,concrete-products"
        }
    },
    "included": [
        {
            "id": "141_29380410",
            "type": "concrete-products",
            "attributes": {
                "sku": "141_29380410",
                "name": "Asus Zenbook US303UB"
            },
            "links": {
                "self": "https://glue-backend.mysprykershop.com/concrete-products/141_29380410?include=picking-list-items,concrete-products"
            }
        },
        {
            "id": "65bb3aec-0a45-5ec6-9b12-bbca6551d87f",
            "type": "picking-list-items",
            "attributes": {
                "quantity": 1,
                "numberOfPicked": 0,
                "numberOfNotPicked": 0,
                "orderItem": {
                    "uuid": "31e21001-e544-5533-9754-51331c8c9ac5",
                    "sku": "141_29380410",
                    "quantity": 1,
                    "name": "Asus Zenbook US303UB",
                    "amountSalesUnit": null
                }
            },
            "relationships": {
                "concrete-products": {
                    "data": [
                        {
                            "id": "141_29380410",
                            "type": "concrete-products"
                        }
                    ]
                }
            },
            "links": {
                "self": "https://glue-backend.mysprykershop.com/picking-list-items/65bb3aec-0a45-5ec6-9b12-bbca6551d87f?include=picking-list-items,concrete-products"
            }
        }
    ]
}
```
</details>

{% endinfo_block %}
