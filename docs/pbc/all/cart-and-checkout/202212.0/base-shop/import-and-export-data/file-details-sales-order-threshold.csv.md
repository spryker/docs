---
title: File details - sales_order_threshold.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-sales-order-thresholdcsv
originalArticleId: 6a897bd7-2a39-4fb0-8eb3-9704e23cd423
redirect_from:
  - /2021080/docs/file-details-sales-order-thresholdcsv
  - /2021080/docs/en/file-details-sales-order-thresholdcsv
  - /docs/file-details-sales-order-thresholdcsv
  - /docs/en/file-details-sales-order-thresholdcsv
  - /docs/pbc/all/cart-and-checkout/202212.0/import-and-export-data/file-details-sales-order-threshold.csv.html
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `sales_order_threshold.csv` file to configure [Sales Order Threshold](/docs/scos/user/features/{{site.version}}/checkout-feature-overview/order-thresholds-overview.html) information in your Spryker Demo Shop.

To import the file, run:

```bash
data:import:sales-order-threshold
```

## Import file parameters

The file should have the following parameters:

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| store | &check; | String |  | Name of the store. |
| currency | &check; | String |  | Currency ISO code. |
| threshold_type_key | &check; | String |  | Identifier of the threshold type. |
| threshold | &check; | Integer |  | Threshold value. |
| fee |  | Integer |   | Threshold fee. |
| message_glossary_key | &check; | String |   | Identifier of the glossary message. |

## Import file dependencies

This file has the following dependencies:

* [currency.csv](/docs/pbc/all/price-management/{{site.version}}/import-and-export-data/file-details-currency.csv.html)
* [glossary.csv](/docs/scos/dev/data-import/{{site.version}}/data-import-categories/commerce-setup/file-details-glossary.csv.html)
* *stores.php* configuration file of the demo shop PHP project

## Import template file and content example

Find the template and an example of the file below:

| FILE | DESCRIPTION |
| --- | --- |
| [sales_order_threshold.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Commerce+Setup/Template+sales_order_threshold.csv) | Exemplary import file with headers only. |
| [sales_order_threshold.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Commerce+Setup/sales_order_threshold.csv) | Exemplary import file with Demo Shop data. |
