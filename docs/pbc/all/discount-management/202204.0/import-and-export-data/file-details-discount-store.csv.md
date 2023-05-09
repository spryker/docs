---
title: File details - discount_store.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-discount-storecsv
originalArticleId: 446bff7a-da3b-4dee-86aa-c245f3529bf1
redirect_from:
  - /2021080/docs/file-details-discount-storecsv
  - /2021080/docs/en/file-details-discount-storecsv
  - /docs/file-details-discount-storecsv
  - /docs/en/file-details-discount-storecsv
  - /docs/scos/dev/data-import/201811.0/data-import-categories/merchandising-setup/discounts/file-details-discount-store.csv.html
  - /docs/scos/dev/data-import/201903.0/data-import-categories/merchandising-setup/discounts/file-details-discount-store.csv.html
  - /docs/scos/dev/data-import/201907.0/data-import-categories/merchandising-setup/discounts/file-details-discount-store.csv.html
  - /docs/scos/dev/data-import/202204.0/data-import-categories/merchandising-setup/discounts/file-details-discount-store.csv.html  
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `discount_store.csv` file to configure Discount Store information in your Spryker Demo Shop.

To import the file, run:

```bash
data:import:discount-store
```

## Import file parameters



| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| discount_key | &check; | String |`discount_key` must be included in the `discount.csv` file. |  |
| store_name | &check; | String |  | The name of the store to which the discount applies. |

## Import file dependencies



* [discount.csv](/docs/pbc/all/discount-management/{{site.version}}/import-and-export-data/file-details-discount.csv.html)
* *stores.php* configuration file of the demo shop PHP project

## Import template file and content example



| FILE | DESCRIPTION |
| --- | --- |
| [discount_store.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Discounts/Template+discount_store.csv) | Exemplary import file with headers only. |
| [discount_store.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Merchandising+Setup/Discounts/discount_store.csv) | Exemplary import file with Demo Shop data. |
