---
title: "File details: product_label_store.csv"
description: Description of the product_label_store.csv import file used to import store relations of product labels.
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-product-label-storecsv
originalArticleId: 6d00793f-81ee-4e04-894f-5650a9e26d17
redirect_from:
  - /2021080/docs/file-details-product-label-storecsv
  - /2021080/docs/en/file-details-product-label-storecsv
  - /docs/file-details-product-label-storecsv
  - /docs/en/file-details-product-label-storecsv
  - /docs/scos/dev/data-import/201811.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-label-store.csv.html
  - /docs/scos/dev/data-import/201903.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-label-store.csv.html
  - /docs/scos/dev/data-import/201907.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-label-store.csv.html
  - /docs/scos/dev/data-import/202005.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-label-store.csv.html
  - /docs/scos/dev/data-import/202204.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-label-store.csv.html
related:
  - title: Product Labels feature overview
    link: docs/pbc/all/product-information-management/page.version/feature-overviews/product-labels-feature-overview.html
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html    
---

This document describes the `product_label_store.csv` file to configure [Product Label](/docs/pbc/all/product-information-management/{{page.version}}/feature-overviews/product-labels-feature-overview.html) and store assignment information in your Spryker Demo Shop.

## Import file dependencies

[product_label.csv](/docs/scos/dev/data-import/{{page.version}}/data-import-categories/merchandising-setup/product-merchandising/file-details-product-label.csv.html).


## Import file parameters

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| name | &check; | String |  | Name of the label. |
| store_name |  | String | | Defines the store relation of the product label. |



## Import template file and content example

| FILE | DESCRIPTION |
| --- | --- |
| [product_label_store.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/Template+product_label_store.csv) | Exemplary import file with headers only. |
| [product_label_store.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/product_label_store.csv) | Exemplary import file with Demo Shop data. |

## Import command

```bash
data:import:product-label-store
```
