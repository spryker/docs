---
title: File details - cms_slot_template.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-cms-slot-templatecsv
originalArticleId: ce6ee377-92eb-4297-9a05-a188447f5865
redirect_from:
  - /2021080/docs/file-details-cms-slot-templatecsv
  - /2021080/docs/en/file-details-cms-slot-templatecsv
  - /docs/file-details-cms-slot-templatecsv
  - /docs/en/file-details-cms-slot-templatecsv
  - /docs/scos/dev/data-import/201811.0/data-import-categories/content-management/file-details-cms-slot-template.csv.html
  - /docs/scos/dev/data-import/202307.0/data-import-categories/content-management/file-details-cms-slot-template.csv.html  
  - /docs/pbc/all/content-management-system/202307.0/import-and-export-data/file-details-cms-slot-template.csv.html  
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `cms_slot_template.csv` file to configure  [CMS Slot Template](/docs/pbc/all/content-management-system/{{page.version}}/base-shop/tutorials-and-howtos/howto-create-cms-templates.html#template-with-slots) information in your Spryker Demo Shop.



## Import file parameters



| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| template_path | &check;  | String |Must be a valid path to a twig template. | Path to the Twig file template. |
| name |  &check;  | String | Human-readable. | Alphabetical identifier of the slot. It will be shown in the Back Office. |
| description |    | String |  | Description of the slot. It will be shown in the Back Office. |





## Import template file and content example



| FILE | DESCRIPTION |
| --- | --- |
| [cms_slot_template.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Content+Management/Template+cms_slot_template.csv) |  Exemplary import file with headers only.  |
| [cms_slot_template.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Content+Management/cms_slot_template.csv) | Exemplary import file with Demo Shop data. |

## Import file command

```bash
data:import:cms-slot-template
```
