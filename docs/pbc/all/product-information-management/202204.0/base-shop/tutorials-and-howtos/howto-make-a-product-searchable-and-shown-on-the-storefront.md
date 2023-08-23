---
title: "HowTo: Make a product searchable and shown on the Storefront"
description: Use the guide to learn about conditions need to be performed to make a product searchable in the online store.
last_updated: Jun 16, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/ht-make-product-shown-on-frontend-by-url
originalArticleId: c8a71f89-7fea-4bd5-9c50-3f372b8af760
redirect_from:
  - /2021080/docs/ht-make-product-shown-on-frontend-by-url
  - /2021080/docs/en/ht-make-product-shown-on-frontend-by-url
  - /docs/ht-make-product-shown-on-frontend-by-url
  - /docs/en/ht-make-product-shown-on-frontend-by-url
  - /v6/docs/ht-make-product-shown-on-frontend-by-url
  - /v6/docs/en/ht-make-product-shown-on-frontend-by-url
  - /v5/docs/ht-make-product-shown-on-frontend-by-url
  - /v5/docs/en/ht-make-product-shown-on-frontend-by-url
  - /v4/docs/ht-make-product-shown-on-frontend-by-url
  - /v4/docs/en/ht-make-product-shown-on-frontend-by-url
  - /v3/docs/ht-make-product-shown-on-frontend-by-url
  - /v3/docs/en/ht-make-product-shown-on-frontend-by-url
  - /v2/docs/ht-make-product-shown-on-frontend-by-url
  - /v2/docs/en/ht-make-product-shown-on-frontend-by-url
  - /v1/docs/ht-make-product-shown-on-frontend-by-url
  - /v1/docs/en/ht-make-product-shown-on-frontend-by-url
  - /docs/scos/dev/tutorials/202005.0/howtos/feature-howtos/howto-make-a-product-searchable-and-shown-on-the-storefront.html
  - /docs/scos/dev/tutorials-and-howtos/howtos/feature-howtos/howto-make-a-product-searchable-and-shown-on-the-storefront.html
related:
  - title: Creating product variants
    link: docs/pbc/all/product-information-management/page.version/base-shop/manage-in-the-back-office/products/manage-product-variants/create-product-variants.html
---

The document describes the flow of making a product searchable and displayed on the Storefront.

There are a number of conditions that must be fulfilled to make your product searchable and shown on Yves by URL. What is important is to make sure that your product meets the following conditions:

* It is assigned to categories. For information about how to assign products to categories, see the [Category](/docs/pbc/all/product-information-management/{{site.version}}/base-shop/manage-in-the-back-office/categories/assign-products-to-categories.html) section.
* It is in stock in the warehouse for the current store. To learn how to check products' availability, see the [Availability](/docs/pbc/all/warehouse-management-system/{{page.version}}/base-shop/manage-in-the-back-office/check-availability-of-products.html) section.
* The product's status is `Active`. To learn how to manage products, including the status change, see the [Products](/docs/pbc/all/product-information-management/{{site.version}}/base-shop/manage-in-the-back-office/products/manage-products.html#activating-products) section.
* It has a price in the current locale. For more details, see the [Products](/docs/pbc/all/product-information-management/{{site.version}}/base-shop/manage-in-the-back-office/products/manage-products.html) section.
* It has been marked as searchable in the Back Office. For more details, see the [Products](/docs/pbc/all/product-information-management/{{site.version}}/base-shop/manage-in-the-back-office/products/manage-product-variants/create-product-variants.html) section.
* It has product variants—an abstract product is not displayed on Yves unless it has product variants. To learn how to create product variants, [Products](/docs/pbc/all/product-information-management/{{site.version}}/base-shop/manage-in-the-back-office/products/manage-product-variants/create-product-variants.html).
