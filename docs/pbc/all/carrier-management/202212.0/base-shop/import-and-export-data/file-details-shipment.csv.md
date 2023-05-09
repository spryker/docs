---
title: File details - shipment.csv
last_updated: Jun 23, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-shipmentcsv
originalArticleId: 213aeaa8-3dd8-43da-870a-5f1174b640e2
redirect_from:
  - /2021080/docs/file-details-shipmentcsv
  - /2021080/docs/en/file-details-shipmentcsv
  - /docs/file-details-shipmentcsv
  - /docs/en/file-details-shipmentcsv
  - /docs/scos/dev/data-import/201811.0/data-import-categories/commerce-setup/file-details-shipment.csv.html
  - /docs/scos/dev/data-import/201903.0/data-import-categories/commerce-setup/file-details-shipment.csv.html
  - /docs/scos/dev/data-import/201907.0/data-import-categories/commerce-setup/file-details-shipment.csv.html
  - /docs/scos/dev/data-import/202204.0/data-import-categories/commerce-setup/file-details-shipment.csv.html
  - /docs/scos/dev/data-import/202212.0/data-import-categories/commerce-setup/file-details-shipment.csv.html
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `shipment.csv` file to configure the [shipment](/docs/scos/user/features/{{site.version}}/shipment-feature-overview.html) information in your Spryker Demo Shop.

To import the file, run

```bash
data:import:shipment
```

## Import file parameters



| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| shipment_method_key| &check; | String | | The identifier of the shipment method. |
| name|  &check; | String | | The name of the shipment method. |
| carrier |  &check; | String |  | The name of the shipment carrier. |
| taxSetName |  &check; | String | | 	The name of the tax set. |
| avalara_tax_code |  | String | | [Avalara tax code](/docs/pbc/all/tax-management/{{page.version}}/tax-management.html#avalara-system-for-automated-tax-compliance) for automated tax calculation. |





## Import template file and content example



| FILE | DESCRIPTION |
| --- | --- |
| [template_shipment.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Commerce+Setup/202109.0/Template_shipment.csv) | Import file template with headers only. |
| [shipment.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Commerce+Setup/202109.0/shipment.csv) | Exemplary import file with the Demo Shop data. |
