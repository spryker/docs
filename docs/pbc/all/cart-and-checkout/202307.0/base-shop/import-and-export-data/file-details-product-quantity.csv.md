---
title: File details - product_quantity.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-product-quantitycsv
originalArticleId: 9959fdc1-deed-48a2-9cea-46c272cb247f
redirect_from:
  - /2021080/docs/file-details-product-quantitycsv
  - /2021080/docs/en/file-details-product-quantitycsv
  - /docs/file-details-product-quantitycsv
  - /docs/en/file-details-product-quantitycsv
  - /docs/scos/dev/data-import/201907.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-quantity.csv.html
  - /docs/scos/dev/data-import/202307.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-quantity.csv.html
  - /docs/pbc/all/cart-and-checkout/202307.0/import-and-export-data/file-details-product-quantity.csv.html
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `product_quantity.csv` file to configure [Product Quantity](/docs/pbc/all/cart-and-checkout/{{site.version}}/base-shop/non-splittable-products-feature-overview.html) Store information in your Spryker Demo Shop.

To import the file, run:

```bash
data:import:product-quantity
```

## Import file parameters

The file should have the following parameters:

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| concrete_sku | &check; | String |  | SKU of the concrete product. |
| quantity_min | Number | String |  |Minimum quantity of the product in cart.  |
| quantity_max | Number | String |  | Maximum quantity of the product in cart. |
| quantity_interval | Number | String |  | Interval restrictions. |

## Import file dependencies

This file has the following dependency: [product_concrete.csv](/docs/pbc/all/product-information-management/{{site.version}}/base-shop/import-and-export-data/products-data-import/file-details-product-concrete.csv.html).

## Import template file and content example

Find the template and an example of the file below:

| FILE | DESCRIPTION |
| --- | --- |
| [product_quantity.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/Template+product_quantity.csv) | Exemplary import file with headers only. |
| [product_quantity.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/product_quantity.csv) | Exemplary import file with headers only. |
