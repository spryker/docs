---
title: File details - cms_block_category_position.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-cms-block-category-postioncsv
originalArticleId: 22c4245e-5056-4bb9-9d77-e932a74c63b9
redirect_from:
  - /2021080/docs/file-details-cms-block-category-postioncsv
  - /2021080/docs/en/file-details-cms-block-category-postioncsv
  - /docs/file-details-cms-block-category-postioncsv
  - /docs/en/file-details-cms-block-category-postioncsv
  - /docs/scos/dev/data-import/202212.0/data-import-categories/content-management/file-details-cms-block-category-postion.csv.html
  - /docs/pbc/all/content-management-system/202212.0/import-and-export-data/file-details-cms-block-category-postion.csv.html
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `cms_block_category_position.csv` file to configure CMS Block Category Position information in your Spryker Demo Shop.

## Import file parameters



| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| cms_block_category_position_name | &check; | String |  |Name of the CMS block category position.  |


## Import template file and content example



| FILE | DESCRIPTION |
| --- | --- |
| [cms_block_category_position.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Content+Management/cms_block_category_position_template.csv) | Exemplary import file with headers only. |
| [cms_block_category_position.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Content+Management/cms_block_category_position.csv) | Exemplary import file with Demo Shop data. |

## Import file command

```bash
data:import:cms-block-category-position
```
