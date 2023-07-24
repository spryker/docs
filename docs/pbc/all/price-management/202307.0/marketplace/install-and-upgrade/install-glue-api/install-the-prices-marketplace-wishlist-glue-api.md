---
title: Install the Prices + Marketplace Wishlist Glue API
description: This document describes how to integrate the Prices + Marketplace Wishlist Glue API feature into a Spryker project.
template: feature-integration-guide-template
redirect_from:
  - /docs/marketplace/dev/feature-integration-guides/202307.0/glue/prices-marketplace-wishlist-feature-integration.html
related:
  - title: Marketplace Wishlist feature walkthrough
    link: docs/marketplace/dev/feature-walkthroughs/page.version/marketplace-wishlist-feature-walkthrough.html
---

This document describes how to integrate the Prices + Marketplace Wishlist Glue API feature into a Spryker project.


## Install feature core

Follow the steps below to install the Prices + Marketplace Wishlist Glue API feature core.

### Prerequisites

To start feature integration, integrate the required features:

| NAME | VERSION | INTEGRATION GUIDE |
| --------------- | ------- | ---------- |
| Marketplace Wishlist | {{page.version}} |[Wishlist feature integration](/docs/marketplace/dev/feature-integration-guides/{{page.version}}/marketplace-wishlist-feature-integration.html) |
| Product Prices API | {{page.version}} |[Glue API: Product Prices feature integration](/docs/pbc/all/price-management/{{site.version}}/base-shop/install-and-upgrade/install-features/install-the-product-price-glue-api.html) |


### 1) Set up behavior

Activate the following plugins:

| PLUGIN | SPECIFICATION | PREREQUISITES | NAMESPACE |
|---|---|---|---|
| PriceProductWishlistItemExpanderPlugin | Expands the `WishlistItem` transfer object with prices. |  | Spryker\Zed\PriceProduct\Communication\Plugin\Wishlist |
| ProductPriceRestWishlistItemsAttributesMapperPlugin | Maps prices to the `RestWishlistItemsAttributes` transfer object. |  | Spryker\Glue\ProductPricesRestApi\Plugin\Wishlist |

**src/Pyz/Zed/Wishlist/WishlistDependencyProvider.php**

```php
<?php
namespace Pyz\Zed\Wishlist;

use Spryker\Zed\PriceProduct\Communication\Plugin\Wishlist\PriceProductWishlistItemExpanderPlugin;
use Spryker\Zed\Wishlist\WishlistDependencyProvider as SprykerWishlistDependencyProvider;

class WishlistDependencyProvider extends SprykerWishlistDependencyProvider
{
    /**
     * @return array<\Spryker\Zed\WishlistExtension\Dependency\Plugin\WishlistItemExpanderPluginInterface>
     */
    protected function getWishlistItemExpanderPlugins(): array
    {
        return [
            new PriceProductWishlistItemExpanderPlugin(),
        ];
    }
}
```

**src/Pyz/Glue/WishlistsRestApi/WishlistsRestApiDependencyProvider.php**

```php
<?php

namespace Pyz\Glue\WishlistsRestApi;

use Spryker\Glue\ProductPricesRestApi\Plugin\Wishlist\ProductPriceRestWishlistItemsAttributesMapperPlugin;
use Spryker\Glue\WishlistsRestApi\WishlistsRestApiDependencyProvider as SprykerWishlistsRestApiDependencyProvider;

class WishlistsRestApiDependencyProvider extends SprykerWishlistsRestApiDependencyProvider
{
    /**
     * @return array<\Spryker\Glue\WishlistsRestApiExtension\Dependency\Plugin\RestWishlistItemsAttributesMapperPluginInterface>
     */
    protected function getRestWishlistItemsAttributesMapperPlugins(): array
    {
        return [
            new ProductPriceRestWishlistItemsAttributesMapperPlugin(),
        ];
    }
}
```

{% info_block warningBox "Verification" %}

Make sure that `PriceProductWishlistItemExpanderPlugin` and `ProductPriceRestWishlistItemsAttributesMapperPlugin` are set up by sending the request `GET https://glue.mysprykershop.com/wishlists/{% raw %}{{wishlistId}}{% endraw %}?include=wishlist-items`. You should get the price product collection within the `attributes` in the response.

{% endinfo_block %}
