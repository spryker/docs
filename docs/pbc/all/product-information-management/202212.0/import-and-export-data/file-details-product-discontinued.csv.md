---
title: File details - product_discontinued.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-product-discontinuedcsv
originalArticleId: 3b2c40f5-ad6d-4ff5-9b65-b058e1ff9419
redirect_from:
  - /2021080/docs/file-details-product-discontinuedcsv
  - /2021080/docs/en/file-details-product-discontinuedcsv
  - /docs/file-details-product-discontinuedcsv
  - /docs/en/file-details-product-discontinuedcsv
  - /docs/scos/dev/data-import/202212.0/data-import-categories/merchandising-setup/product-merchandising/file-details-product-discontinued.csv.html
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `product_discontinued.csv` file to configure [Discontinued Product](/docs/scos/user/features/{{page.version}}/product-feature-overview/discontinued-products-overview.html) information in your Spryker Demo Shop.

## Import file dependencies

[product_concrete.csv](/docs/pbc/all/product-information-management/{{page.version}}/import-and-export-data/products-data-import/file-details-product-concrete.csv.html)


## Import file parameters

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| sku_concrete | &check; | String |N/A* | SKU of the concrete discontinued product. |
| note.{ANY_LOCALE_NAME}*<br>Example value: *note.en_US* |  | String |N/A | Note translated into the specified locale (US for our example).  |

*ANY_LOCALE_NAME: Locale date is dynamic in data importers. It means that ANY_LOCALE_NAME postfix can be changed, removed, and any number of columns with different locales can be added to the CSV files.



## Import template file and content example

| FILE | DESCRIPTION |
| --- | --- |
| [product_discontinued.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/Template+product_discontinued.csv) | Exemplary import file with headers only. |
| [product_discontinued.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/product_discontinued.csv) | Exemplary import file with Demo Shop data. |

## Import command

```bash
data:import:product-discontinued
```
