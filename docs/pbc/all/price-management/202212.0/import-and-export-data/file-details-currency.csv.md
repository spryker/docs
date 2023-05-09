---
title: File details - currency.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-currencycsv
originalArticleId: d4ee04b4-8159-4846-9c3a-d98c28423b5c
redirect_from:
  - /2021080/docs/file-details-currencycsv
  - /2021080/docs/en/file-details-currencycsv
  - /docs/file-details-currencycsv
  - /docs/en/file-details-currencycsv
  - /docs/scos/dev/data-import/202212.0/data-import-categories/commerce-setup/file-details-currency.csv.html
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `currency.csv` file to configure [Currency](/docs/pbc/all/price-management/{{site.version}}/extend-and-customize/multiple-currencies-per-store-configuration.html) information in your Spryker Demo Shop.

To import the file, run:

```bash
data:import:currency
```

## Import file parameters



| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| iso_code | &check; | String |   | Currency ISO code. <br>For more details check [ISO 4217 CURRENCY CODES](https://www.iso.org/iso-4217-currency-codes.html).  |
| currency_symbol | &check; | String |   | Currency symbol. |
| name | &check; | String |   | Currency name. |





## Additional information

It is recommended to fill all three columns, when adding a new record, except if the “currency” being added is not an ISO standard currency (for example, system of points, or product/service exchange, etc.).

Default currency might be set up when setting up the store. Check [here](https://github.com/spryker-shop/b2c-demo-shop/blob/master/config/Shared/stores.php#L38).

## Import template file and content example



| FILE | DESCRIPTION |
| --- | --- |
| [currency.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Commerce+Setup/Template+currency.csv) | Exemplary import file with headers only. |
| [currency.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Commerce+Setup/currency.csv) | Exemplary import file with Demo Shop data. |
