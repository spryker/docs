---
title: File details - cms_block.csv
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-cms-blockcsv
originalArticleId: 2fde5c8a-6217-4151-a511-23b71759feb0
redirect_from:
  - /2021080/docs/file-details-cms-blockcsv
  - /2021080/docs/en/file-details-cms-blockcsv
  - /docs/file-details-cms-blockcsv
  - /docs/en/file-details-cms-blockcsv
  - /docs/scos/dev/data-import/201811.0/data-import-categories/content-management/file-details-cms-block.csv.html
  - /docs/scos/dev/data-import/202212.0/data-import-categories/content-management/file-details-cms-block.csv.html  
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `cms_block.csv` file to configure [CMS Block](/docs/pbc/all/content-management-system/{{page.version}}/cms-feature-overview/cms-blocks-overview.html) information on your Spryker Demo Shop.

## Import file command

```bash
data:import:cms-block
```

## Import file parameters

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| block_key | &check; | String |  |Block key identifier  |
| block_name | &check; | String |Must be unique. Human-readable name. | Name of the block. |
| template_name |  | String |  | Alphabetical identifier of the slot. It will be shown in the Back Office. |
| template_path |  | String |Must be a valid path to a twig template. | Path to the Twig file template. |
| active |  | Boolean |<ul><li>Inactive = 0</li><li>Active = 1</li><li>If empty during the import, the block will be imported as inactive.</li></ul> | Indicates if the block is active or inactive. |
| placeholder.title.{ANY_LOCALE_NAME}*<br>Example value: *placeholder.title.en_US* |  | String |  | Placeholder for block title, translated into the specified locale (US for our example). |
| placeholder.description.{ANY_LOCALE_NAME}*<br>Example value: *placeholder.description.en_US* |  | String |  | Placeholder for block description, translated into the specified locale (US for our example). |
| placeholder.link.{ANY_LOCALE_NAME}*<br>Example value: *placeholder.link.en_US* |  | String |  | Placeholder for block link, translated into the specified locale (US for our example). |
| placeholder.content.{ANY_LOCALE_NAME}*<br>Example value: *placeholder.content.en_US* |  | String |  | Placeholder for block content, translated into the specified locale (US for our example). |

*ANY_LOCALE_NAME: Locale date is dynamic in data importers. It means that ANY_LOCALE_NAME postfix can be changed, removed, and any number of columns with different locales can be added to the CSV files.



## Import template file and content example



| FILE | DESCRIPTION |
| --- | --- |
| [cms_block.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Content+Management/Template+cms_block.csv) | Exemplary import file with headers only. |
| [cms_block.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Content+Management/cms_block.csv) | Exemplary import file with Demo Shop data. |
