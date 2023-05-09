---
title: "File details: product_abstract_store.csv"
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-product-abstract-storecsv
originalArticleId: 289b16ad-bb98-40cb-80c6-cfdef692687f
redirect_from:
  - /2021080/docs/file-details-product-abstract-storecsv
  - /2021080/docs/en/file-details-product-abstract-storecsv
  - /docs/file-details-product-abstract-storecsv
  - /docs/en/file-details-product-abstract-storecsv
  - /docs/scos/dev/data-import/202204.0/data-import-categories/catalog-setup/products/file-details-product-abstract-store.csv.html
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `product_abstract_store.csv` file to configure Product Abstract Store information in your Spryker Demo Shop.

## Import file dependencies

* [product_abstract.csv](/docs/pbc/all/product-information-management/{{page.version}}/import-and-export-data/products-data-import/file-details-product-abstract.csv.html)
* *stores.php* configuration file of the demo shop PHP project


## Import file parameters

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| abstract_sku | &check; | String | Must be unique. | SKU identifier of the abstract product. |
| store_name | &check; | String |  | Name of the store that has this product. |


## Import template file and content example

| FILE | DESCRIPTION |
| --- | --- |
| [product_abstract_store.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Catalog+Setup/Products/Template+product_abstract_store.csv) | Exemplary import file with headers only. |
| [product_abstract_store.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Catalog+Setup/Products/product_abstract_store.csv) | Exemplary import file with Demo Shop data. |

## Import command

```bash
data:import:product-abstract-store
```
