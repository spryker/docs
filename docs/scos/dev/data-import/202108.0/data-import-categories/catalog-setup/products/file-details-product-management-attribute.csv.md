---
title: File details - product_management_attribute.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-product-management-attributecsv
originalArticleId: f812b029-e27e-43e7-a6a0-a6db56be3a30
redirect_from:
  - /2021080/docs/file-details-product-management-attributecsv
  - /2021080/docs/en/file-details-product-management-attributecsv
  - /docs/file-details-product-management-attributecsv
  - /docs/en/file-details-product-management-attributecsv
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `product_management_attribute.csv` file to configure [product attribute](/docs/scos/user/features/{{page.version}}/product-feature-overview/product-feature-overview.html) information in your Spryker Demo Shop.

To import the file, run:

```bash
data:import:product-management-attribute
```

## Import file parameters

The file should have the following parameters:

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| key | &check; | String |   | Key identifier of the product attribute. |
| input_type | &check; | String | Value from a pre-defined list. | Input type of the product attribute, for example, text, number, select, etc. |
| allow_input |  | String |  *yes/no* field. Will be set to *no* if an empty value is provided. |Indicates if custom values can be entered in this product attribute.  |
| is_multiple | No | String | *yes/no* field. Will be set to *no* if an empty value is provided. |Indicates if the attribute can have multiple values.  |
| values |  | String |  | Selectable values. Field *values* is a string defining possible attribute values, separated by commas. For example, "16 GB, 32 GB, 64 GB, 128 GB" means that attribute can accept values "16 GB", "32 GB", "64 GB", "128 GB". |
| key_translation.en_US |  | String |  | Translation attribute key to the locale US language. |
| key_translation.de_DE |  | String |  | Translation attribute key to the locale DE language. |
| value_translations.en_US |  | String |  | Translation attribute value to the locale US language. |
| value_translations.de_DE |  | String |  | Translation attribute value to the locale DE language. |

## Import file dependencies

This file has the following dependencies:

* [ product_attribute_key.csv](/docs/scos/dev/data-import/{{page.version}}/data-import-categories/catalog-setup/products/file-details-product-attribute-key.csv.html)
* [glossary.csv](/docs/scos/dev/data-import/{{page.version}}/data-import-categories/commerce-setup/file-details-glossary.csv.html)

## Import template file and content example

Find the template and an example of the file below:

| FILE | DESCRIPTION |
| --- | --- |
| [product_management_attribute.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Catalog+Setup/Products/Template+product_management_attribute.csv) | Exemplary import file with headers only. |
| [product_management_attribute.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Catalog+Setup/Products/product_management_attribute.csv) | Exemplary import file with Demo Shop data. |
