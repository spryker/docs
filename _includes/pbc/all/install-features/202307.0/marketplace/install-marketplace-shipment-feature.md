This document describes how to integrate the Marketplace Shipment feature into a Spryker project.

## Install feature core

Follow the steps below to install the Marketplace Shipment feature core.

### Prerequisites

To start feature integration, integrate the required features:

| NAME | VERSION | INTEGRATION GUIDE |
|-|-|-|
| Merchant | {{page.version}} | [Merchant feature integration](/docs/pbc/all/merchant-management/{{page.version}}/marketplace/install-and-upgrade/install-features/install-the-marketplace-merchant-feature.html) |
| Shipment | {{page.version}} | [Shipment feature integration](/docs/pbc/all/carrier-management/{{site.version}}/base-shop/install-and-upgrade/install-features/install-the-shipment-feature.html) |


### 1) Install the required modules using Composer

Install the required modules:

```bash
composer require spryker-feature/marketplace-shipment:"{{page.version}}" --update-with-dependencies
```

{% info_block warningBox "Verification" %}

Make sure that the following modules were installed:

| MODULE | EXPECTED DIRECTORY |
|-|-|
| MerchantShipment | vendor/spryker/merchant-shipment |
| MerchantShipmentGui | vendor/spryker/merchant-shipment-gui |

{% endinfo_block %}

### 2) Set up configuration

Add the following configuration to your project:

| CONFIGURATION | SPECIFICATION | NAMESPACE |
|-|-|-|
| ShipmentConfig::getShipmentHashFields() | Used to group items by shipment using merchant reference. | \Pyz\Service\Shipment |

**src/Pyz/Service/Shipment/ShipmentConfig.php**

```php
<?php

namespace Pyz\Service\Shipment;

use Generated\Shared\Transfer\ShipmentTransfer;
use Spryker\Service\Shipment\ShipmentConfig as SprykerShipmentConfig;

class ShipmentConfig extends SprykerShipmentConfig
{
    /**
     * @return array<string>
     */
    public function getShipmentHashFields(): array
    {
        return array_merge(parent::getShipmentHashFields(), [ShipmentTransfer::MERCHANT_REFERENCE]);
    }
}
```

{% info_block warningBox "Verification" %}

Place an order and check that items are grouped by merchant shipment in backoffice.

{% endinfo_block %}

### 3) Set up the database schema and transfer definitions

Apply the database changes and generate entity and transfer changes:

```bash
console transfer:generate
console propel:install
console transfer:generate
```

{% info_block warningBox "Verification" %}

Verify that the following changes have been applied by checking your database:

| DATABASE ENTITY | TYPE | EVENT |
|-|-|-|
| spy_sales_shipment.merchant_reference | column | created |

Make sure that the following changes were applied in transfer objects:

| TRANSFER  | TYPE  | EVENT | PATH  |
|-|-|-|-|
| MerchantShipmentCriteria | class | created | src/Generated/Shared/Transfer/MerchantShipmentCriteria |
| Shipment.merchantReference | property | created | src/Generated/Shared/Transfer/ShipmentTransfer |

{% endinfo_block %}

### 4) Set up behavior

Enable the following behaviors by registering the plugins:

| PLUGIN | DESCRIPTION | PREREQUISITES | NAMESPACE |
|-|-|-|-|
| MerchantShipmentOrderItemTemplatePlugin | Shows merchant shipment in shipment section of the ShipmentGui::SalesController |  | Spryker\Zed\MerchantShipmentGui\Communication\ShipmentGui |

**src/Pyz/Zed/ShipmentGui/ShipmentGuiDependencyProvider.php**

```php
<?php

/**
 * This file is part of the Spryker Suite.
 * For full license information, please view the LICENSE file that was distributed with this source code.
 */

namespace Pyz\Zed\ShipmentGui;

use Spryker\Zed\MerchantShipmentGui\Communication\ShipmentGui\MerchantShipmentOrderItemTemplatePlugin;
use Spryker\Zed\ShipmentGui\ShipmentGuiDependencyProvider as SprykerShipmentGuiDependencyProvider;

class ShipmentGuiDependencyProvider extends SprykerShipmentGuiDependencyProvider
{
    /**
     * @return array<\Spryker\Zed\ShipmentGuiExtension\Dependency\Plugin\ShipmentOrderItemTemplatePluginInterface>
     */
    protected function getShipmentOrderItemTemplatePlugins(): array
    {
        return [
            new MerchantShipmentOrderItemTemplatePlugin(),
        ];
    }
}
```

## Related features

| FEATURE | REQUIRED FOR THE CURRENT FEATURE| INTEGRATION GUIDE |
|-|-|-|
| Marketplace Shipment + Cart | | [Marketplace Shipment + Cart feature integration](/docs/pbc/all/carrier-management/{{page.version}}/marketplace/install-features/install-the-marketplace-shipment-cart-feature.html) |
| Marketplace Shipment + Checkout | | [Marketplace Shipment + Checkout feature integration](/docs/pbc/all/carrier-management/{{page.version}}/marketplace/install-features/install-the-marketplace-shipment-checkout-feature.html) |
| Marketplace Shipment + Customer | | [Marketplace Shipment + Customer feature integration](/docs/pbc/all/carrier-management/{{page.version}}/marketplace/install-features/install-marketplace-shipment-customer-feature.html) |
