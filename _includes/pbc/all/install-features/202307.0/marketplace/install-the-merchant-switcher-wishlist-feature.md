

This document describes how to integrate the Merchant Switcher + Wishlist feature into a Spryker project.

## Install feature core

Follow the steps below to install the Merchant Switcher + Wishlist feature core.

### Prerequisites

Install the required features:

| NAME | VERSION | INTEGRATION GUIDE  |
|-|-|-|
| Merchant Switcher | {{page.version}} | [Merchant Switcher feature integration](/docs/pbc/all/merchant-management/{{page.version}}/marketplace/install-and-upgrade/install-features/install-the-merchant-switcher-feature.html)|
| Marketplace Wishlist | {{page.version}} | [Marketplace Wishlist feature integration](/docs/pbc/all/shopping-list-and-wishlist/{{page.version}}/marketplace/install-and-upgrade/install-features/install-the-marketplace-wishlist-feature.html) |

### 1) Set up behavior

Enable the following behaviors by registering the plugins:

| PLUGIN | DESCRIPTION | PREREQUISITES | NAMESPACE |
|-|-|-|-|
| SingleMerchantWishlistReloadItemsPlugin | Expands `WishlistItemMetaFormType` with the hidden fields for the `merchant_reference` and the `product_offer_reference`. |  | Spryker\Zed\MerchantSwitcher\Communication\Plugin\Wishlist |
| SingleMerchantWishlistItemsValidatorPlugin | Expands `WishlistItemMetaFormType` with the hidden fields for the `merchant_reference` and the `product_offer_reference`. |  | Spryker\Zed\MerchantSwitcher\Communication\Plugin\Wishlist |

```php
<?php

namespace Pyz\Zed\Wishlist;

use Spryker\Zed\MerchantSwitcher\Communication\Plugin\Wishlist\SingleMerchantWishlistItemsValidatorPlugin;
use Spryker\Zed\MerchantSwitcher\Communication\Plugin\Wishlist\SingleMerchantWishlistReloadItemsPlugin;

class WishlistDependencyProvider extends SprykerWishlistDependencyProvider
{
 /**
  * @return array<\Spryker\Zed\WishlistExtension\Dependency\Plugin\WishlistReloadItemsPluginInterface>
  */
 protected function getWishlistReloadItemsPlugins(): array
 {
     return [
         new SingleMerchantWishlistReloadItemsPlugin(),
     ];
 }

 /**
  * @return array<\Spryker\Zed\WishlistExtension\Dependency\Plugin\WishlistItemsValidatorPluginInterface>
  */
 protected function getWishlistItemsValidatorPlugins(): array
 {
     return [
         new SingleMerchantWishlistItemsValidatorPlugin(),
     ];
 }
}
```
