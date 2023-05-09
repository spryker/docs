---
title: File details - product_relation.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-product-relationcsv
originalArticleId: ce1a13ce-5d62-4e75-9af5-912210f3a8f0
redirect_from:
  - /2021080/docs/file-details-product-relationcsv
  - /2021080/docs/en/file-details-product-relationcsv
  - /docs/file-details-product-relationcsv
  - /docs/en/file-details-product-relationcsv
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `product_relation.csv` file to configure [Product Relation](/docs/scos/user/features/{{page.version}}/product-relations-feature-overview.html) information in your Spryker Demo Shop.

To import the file, run:

```bash
data:import:product-relation
```

## Import file parameters

The file should have the following parameters:

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| product | &check; | String |  | SKU of the abstract product. |
| relation_type |  | String |  | Type of relation. |
| rule |  | String |  | Query which defines the relation between the product and the other products. |
| product_relation_key | &check; | String |  | Key that is used to assign store relations. |
| is_active |  | Integer |  | Defines if the product relation is active. |
| is_rebuild_scheduled |  | Integer |  | Defines if the list of related products should be regularly updated by running a cronjob. |

## Import file dependencies

This file has the following dependency: [product_abstract.csv](/docs/scos/dev/data-import/{{page.version}}/data-import-categories/catalog-setup/products/file-details-product-abstract.csv.html).

## Import template file and content example

Find the template and an example of the file below:

| FILE | DESCRIPTION |
| --- | --- |
| [product_relation.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/Template+product_relation.csv) | Exemplary import file with headers only. |
| [product_relation.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/product_relation.csv) | Exemplary import file with headers only. |
