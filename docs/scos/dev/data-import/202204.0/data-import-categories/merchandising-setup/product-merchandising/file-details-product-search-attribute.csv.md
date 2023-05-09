---
title: "File details: product_search_attribute.csv"
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-product-search-attributecsv
originalArticleId: 65570cb4-dec5-4f90-85f2-3d22493d874c
redirect_from:
  - /2021080/docs/file-details-product-search-attributecsv
  - /2021080/docs/en/file-details-product-search-attributecsv
  - /docs/file-details-product-search-attributecsv
  - /docs/en/file-details-product-search-attributecsv
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `product_search_attribute.csv` file to configure Product Search Attribute information in your Spryker Demo Shop.

To import the file, run:

```bash
data:import:product-search-attribute
```

## Import file parameters

The file must have the following parameters:

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| key | &check; | String |N/A* | Key identifier string of the product search attribute. |
| filter_type |  | String |N/A | Type of search filter, Elasticsearch-specific. |
| position |  | Number |N/A | Position of the product search attribute, Elasticsearch specific. |
| key.{ANY_LOCALE_NAME}*<br>Example value: *key.en_US*  | &check; | String |N/A | Key identifier string of the product search attribute, translated in the specified locale US for our example). |

*ANY_LOCALE_NAME: Locale date is dynamic in data importers. It means that ANY_LOCALE_NAME postfix can be changed or removed, and any number of columns with different locales can be added to the CSV files.

## Import file dependencies

This file has the following dependency: [product_attribute_key.csv](/docs/pbc/all/product-information-management/{{page.version}}/import-and-export-data/products-data-import/file-details-product-attribute-key.csv.html)

## Additional information

The attribute key is previously loaded from `productattributekey.csv`, which can be translated into the key.* fields.

## Import template file and content example

The following table contains the template and an example of the file:

| FILE | DESCRIPTION |
| --- | --- |
| [product_search_attribute.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/Template+product_search_attribute.csv) | Exemplary import file with headers only. |
| [product_search_attribute.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Product+Merchandising/product_search_attribute.csv) | Exemplary import file with headers only. |
