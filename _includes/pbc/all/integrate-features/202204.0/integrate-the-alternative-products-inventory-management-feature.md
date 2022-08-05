

## Install feature core

### Prerequisites

To start feature integration, review and install the necessary features:

| NAME | VERSION |
|---|---|
|Alternative Products|{{site.version}}|
|Inventory Management|{{site.version}}|

### 1) Set up behavior

Enable the following behaviors by registering the plugins:

| PLUGIN | SPECIFICATION | PREREQUISITES | NAMESPACE |
|---|---|---|---|
|AvailabilityCheckAlternativeProductApplicablePlugin|Checks if product alternatives should be shown for the product.|None|`Spryker\Zed\Availability\Communication\Plugin\ProductAlternative|
|AvailabilityCheckAlternativeProductApplicablePlugin|Checks if product alternatives should be shown for the product.|Expects SKU and `IdProductAbstract` to be set for the ProductViewTransfer.|Spryker\Client\AvailabilityStorage\Plugin\ProductAlternativeStorage|

**src/Pyz/Client/ProductAlternativeStorage/ProductAlternativeStorageDependencyProvider.php**

```php
<?php

namespace Pyz\Client\ProductAlternativeStorage;

use Spryker\Client\AvailabilityStorage\Plugin\ProductAlternativeStorage\AvailabilityCheckAlternativeProductApplicablePlugin;
use Spryker\Client\ProductAlternativeStorage\ProductAlternativeStorageDependencyProvider as SprykerProductAlternativeStorageDependencyProvider;

class ProductAlternativeStorageDependencyProvider extends SprykerProductAlternativeStorageDependencyProvider
{
	/**
	 * @return \Spryker\Client\ProductAlternativeStorageExtension\Dependency\Plugin\AlternativeProductApplicablePluginInterface[]
	 */
	protected function getAlternativeProductApplicableCheckPlugins(): array
	{
		return [
			new AvailabilityCheckAlternativeProductApplicablePlugin(),
		];
	}
}
```

**src/Pyz/Zed/ProductAlternative/ProductAlternativeDependencyProvider.php**

```php
<?php

namespace Pyz\Zed\ProductAlternative;

use Spryker\Zed\Availability\Communication\Plugin\ProductAlternative\AvailabilityCheckAlternativeProductApplicablePlugin;
use Spryker\Zed\ProductAlternative\ProductAlternativeDependencyProvider as SprykerProductAlternativeDependencyProvider;

class ProductAlternativeDependencyProvider extends SprykerProductAlternativeDependencyProvider
{
	/**
	 * @return \Spryker\Zed\ProductAlternativeExtension\Dependency\Plugin\AlternativeProductApplicablePluginInterface[]
	 */
	protected function getAlternativeProductApplicablePlugins(): array
	{
		return [
			new AvailabilityCheckAlternativeProductApplicablePlugin(),
		];
	}
}
```

{% info_block warningBox “Verification” %}

Make sure that you can see alternatives for not available products on the product detail page.

{% endinfo_block %}
