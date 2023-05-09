---
title: File details - mime_type.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-mime-typecsv
originalArticleId: cec9c3b6-fb1c-4d60-829c-cf37d9d54404
redirect_from:
  - /2021080/docs/file-details-mime-typecsv
  - /2021080/docs/en/file-details-mime-typecsv
  - /docs/file-details-mime-typecsv
  - /docs/en/file-details-mime-typecsv
  - /docs/scos/dev/data-import/202204.0/data-import-categories/miscellaneous/file-details-mime-type.csv.html  
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `mime_type.csv` file used to configure MIME Type information in your Spryker Demo Shop. For more information about MIME types, see [Reference information: MIME TYPE](https://github.com/spryker/spryker-docs/blob/review-digital-asset-management/docs/pbc/all/content-management-system/{{page.version}}/manage-in-the-back-office/add-and-edit-mime-types.md#reference-information-mime-type).

## Prerequisites

This file does not exist by default on the project level. To override the default `mime_type.csv` file of the `file-manager-data-import` module, create the file in the `data/import` folder.

## Import file parameters

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| name | &check; | String | Must be a valid MIME type. | Name of the MIME type. |
| is_allowed | &check; | Boolean |<ul><li>True = 1</li><li>False = 0</li></ul> | Indicates whether the MIME type is allowed or not. |


## Import template file and content example

| FILE | DESCRIPTION |
| --- | --- |
| [mime_type.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Miscellaneous/Template+mime_type.csv) | Example import file with headers only. |
| [mime_type.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Miscellaneous/mime_type.csv) | Example import file with Demo Shop data. |

## Import file command

```bash
data:import:mime-type
```
