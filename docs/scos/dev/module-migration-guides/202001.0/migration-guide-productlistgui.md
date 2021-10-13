---
title: Migration Guide - ProductListGui
description: This migration guide contains steps on migrating  ProductListGui to the major release versions.
template: module-migration-guide-template
originalLink: https://documentation.spryker.com/v4/docs/migration-guide-product-list-gui
originalArticleId: 5efa6ddf-f354-4a40-b7ea-9341f31ce38c
redirect_from:
  - /v4/docs/migration-guide-product-list-gui
  - /v4/docs/en/migration-guide-product-list-gui
related:
  - title: Migration Guide - MerchantRelationshipProductListGui
    link: docs/scos/dev/module-migration-guides/page.version/migration-guide-merchantrelationshipproductlistgui.html
---

## Upgrading from Version 1.* to Version 2.0.0
The main point of the `ProductListGui` v2.0.0 is the following: exclusive ownership for product lists was removed from the merchant relations.

Instead of this, an enhanced ownership concept was introduced to allow multiple different domain entities to own a product list.

Other changes are listed below:

* Adjusted `EditController::indexAction()` to provide aggregation tabs for the twig template.
* Introduced `ProductConcreteRelationConfigurableBundleTemplateSlotEditSubTabsProviderPlugin`.
* Introduced ProductConcreteRelationConfigurableBundleTemplateSlotEditTablesProviderPlugin.
* Introduced `ProductConcreteRelationCsvConfigurableBundleTemplateSlotEditFormFileUploadHandlerPlugin`.
* Introduced `ProductListManagementConfigurableBundleTemplateSlotEditFormDataProviderExpanderPlugin`.
* Introduced `ProductListManagementConfigurableBundleTemplateSlotEditFormExpanderPlugin`.
* Introduced `ProductListManagementConfigurableBundleTemplateSlotEditTabsExpanderPlugin`.
* Replaced `ProductListFacade::deleteProductList()` usage with `ProductListFacade::removeProductList()` in `DeleteController::confirmAction()`.
* Introduced extension point to inject buttons for the product list table.
* Adjusted UI to see the owner domain entities for each product list.
* Adjusted deletion logic so that it is not possible to delete a product list if it has any owner domain entity.
* Introduced extension point to define the ownership over product list by another domain entity.
* Deprecated `ProductListOwnerTypeFormExpanderPluginInterface` to allow multiple owners concept.

{% info_block warningBox "Note" %}
Keep in mind, that the Products Lists feature with the `ProductListGui` module makes sense only in connection with modules `MerchantRelationshipProductListGui` v. 2.0.0 and `ConfigurableBundleGui`.
{% endinfo_block %}

**To upgrade to the new version of the module, do the following:**

1. Update `ProductListGui` module version and its dependencies by running the following command:
```bash
composer require spryker/product-list-gui:"^2.0.0" --update-with-dependencies
```
2. Update the transfer objects:
```bash
console transfer:generate
```
3. Generate translator cache by running the following command to get the latest Zed translations:
```bash
console translator:generate-cache
```
{% info_block infoBox "Info" %}
If your project code contains any `ProductListFacade::deleteProductList(
{% endinfo_block %}` methods usage, then update them to be `ProductListFacade::removeProductList()` since the old method is deprecated now and should not be used anymore.)
{% info_block infoBox "Info" %}
Avoid using of the plugins implementing `ProductListOwnerTypeFormExpanderPluginInterface`, since the last one is deprecated and not relevant anymore.
{% endinfo_block %}
4. Remove following methods from `src/Pyz/Zed/ProductListGui/ProductListGuiDependencyProvider.php` (if any present):

* `getProductListOwnerTypeFormExpanderPlugins`
* `getProductListTableConfigExpanderPlugins`
* `getProductListTableQueryCriteriaExpanderPlugins`
* `getProductListTableDataExpanderPlugins`
* `getProductListTableHeaderExpanderPlugins`

5.  If your project has any domain entities that use product list (e.g. *Configurable Bundle*, *Merchant Relationship*, etc), add the respective plugins to the dependency provider:
```php
<?php

namespace Pyz\Zed\ProductListGui;

use Spryker\Zed\ConfigurableBundleGui\Communication\Plugin\ProductListGui\ConfigurableBundleTemplateListProductListTopButtonsExpanderPlugin;
use Spryker\Zed\ConfigurableBundleGui\Communication\Plugin\ProductListGui\ConfigurableBundleTemplateProductListUsedByTableExpanderPlugin;
use Spryker\Zed\MerchantRelationshipProductListGui\Communication\Plugin\ProductListGui\MerchantRelationListProductListTopButtonsExpanderPlugin;
use Spryker\Zed\MerchantRelationshipProductListGui\Communication\Plugin\ProductListGui\MerchantRelationshipProductListUsedByTableExpanderPlugin;
use Spryker\Zed\ProductListGui\ProductListGuiDependencyProvider as SprykerProductListGuiDependencyProvider;

class ProductListGuiDependencyProvider extends SprykerProductListGuiDependencyProvider
{
    /**
     * @return \Spryker\Zed\ProductListGuiExtension\Dependency\Plugin\ProductListTopButtonsExpanderPluginInterface[]
     */
    protected function getProductListTopButtonsExpanderPlugins(): array
    {
        return [
            new ConfigurableBundleTemplateListProductListTopButtonsExpanderPlugin(),
            new MerchantRelationListProductListTopButtonsExpanderPlugin(),
        ];
    }

    /**
     * @return \Spryker\Zed\ProductListGuiExtension\Dependency\Plugin\ProductListUsedByTableExpanderPluginInterface[]
     */
    protected function getProductListUsedByTableExpanderPlugins(): array
    {
        return [
            new ConfigurableBundleTemplateProductListUsedByTableExpanderPlugin(),
            new MerchantRelationshipProductListUsedByTableExpanderPlugin(),
        ];
    }
}
```

* `ProductListTopButtonsExpanderPluginInterface[]` plugins are responsible for adding the top button to the product list index page which leads to the domain entity page which uses the product list for its purpose.
* `ProductListUsedByTableExpanderPluginInterface[]` plugins are responsible for expanding table at Used By tab at Product List Edit page. This table contains a list of domain entities that use exact product list.

6. Run the following command to apply JS changes:
```bash
console frontend:zed:build
```

*Estimated migration time: 1-2 hours*
