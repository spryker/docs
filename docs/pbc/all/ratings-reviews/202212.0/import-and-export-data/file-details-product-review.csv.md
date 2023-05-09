---
title: File details- product_review.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-product-reviewcsv
originalArticleId: f404c07b-fa94-4e85-97e1-7aac3f282de8
redirect_from:
  - /2021080/docs/file-details-product-reviewcsv
  - /2021080/docs/en/file-details-product-reviewcsv
  - /docs/file-details-product-reviewcsv
  - /docs/en/file-details-product-reviewcsv
  - /docs/scos/dev/data-import/201811.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-review.csv.html
  - /docs/scos/dev/data-import/201903.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-review.csv.html
  - /docs/scos/dev/data-import/201907.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-review.csv.html
  - /docs/scos/dev/data-import/202212.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-review.csv.html
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `product_review.csv` file to configure [Product Review](/docs/scos/user/features/{{site.version}}/product-rating-and-reviews-feature-overview.html) information in your Spryker Demo Shop.

## Import file dependencies

[product_abstract.csv](/docs/pbc/all/product-information-management/{{site.version}}/import-and-export-data/products-data-import/file-details-product-abstract.csv.html).


## Import file parameters

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| customer_reference | &check; | String |  | Reference identifier of the customer. |
| abstract_product_sku | &check; | String |  | SKU of the abstract product. |
| locale_name |  | String |  | Identification of the locale of the review. |
| nickname |  | String |  | Nickname of the review owner. |
| summary |  | String |  | Summary of the review. |
| description |  | String |  | Description of the review. |
| rating | &check; | Number |  | Review rating. |
| status | &check; | String | Possible values: *pending*, *approved*,  *rejected*. | Review status. |


## Import template file and content example

| FILE | DESCRIPTION |
| --- | --- |
| [product_review.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/Template+product_review.csv) | Exemplary import file with headers only. |
| [product_review.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/product_review.csv) | Exemplary import file with headers only. |

## Import command

```bash
data:import:product-review
```
