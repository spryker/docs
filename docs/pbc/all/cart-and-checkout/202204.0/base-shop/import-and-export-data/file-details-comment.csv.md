---
title: "File details: comment.csv"
last_updated: Jun 16, 2021
template: data-import-template
originalLink: https://documentation.spryker.com/2021080/docs/file-details-commentcsv
originalArticleId: 2748359a-d71e-4878-a3d9-ae305f124192
redirect_from:
  - /2021080/docs/file-details-commentcsv
  - /2021080/docs/en/file-details-commentcsv
  - /docs/file-details-commentcsv
  - /docs/en/file-details-commentcsv
  - /docs/scos/dev/data-import/201907.0/data-import-categories/miscellaneous/file-details-comment.csv.html
  - /docs/scos/dev/data-import/202204.0/data-import-categories/miscellaneous/file-details-comment.csv.html  
related:
  - title: Execution order of data importers in Demo Shop
    link: docs/scos/dev/data-import/page.version/demo-shop-data-import/execution-order-of-data-importers-in-demo-shop.html
---

This document describes the `comment.csv` file to configure [Comment](/docs/pbc/all/cart-and-checkout/{{site.version}}/base-shop/comments-feature-overview.html)  information in your Spryker Demo Shop.

To import the file, run:

```bash
data:import:comment
```

## Import file parameters

The file must have the following parameters:

| PARAMETER | REQUIRED | TYPE | REQUIREMENTS OR COMMENTS | DESCRIPTION |
| --- | --- | --- | --- | --- |
| message_key |  | String |  | Identifier of the message with the comment. |
| owner_type |  | String |  | Owner type that issued the comment. |
| owner_key |  | String |  | Owner key identifier who issued the comment. |
| customer_reference |  | String |  |Reference of the customer.  |
| message |  | String |  |Message with the comment.  |

## Import file dependencies

This file has the following dependency: [customer.csv](/docs/scos/dev/data-import/{{site.version}}/data-import-categories/commerce-setup/file-details-customer.csv.html).

## Import template file and content example

The following table contains the template and an example of the file:

| FILE | DESCRIPTION |
| --- | --- |
| [comment.csv template](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Miscellaneous/Template+comment.csv) | Exemplary import file with headers only. |
| [comment.csv](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Back-End/Data+Manipulation/Data+Ingestion/Data+Import/Data+Import+Categories/Miscellaneous/comment.csv) | Exemplary import file with Demo Shop data. |
