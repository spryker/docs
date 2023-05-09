---
title: Product Approval Process feature overview
description: Product Approval Process feature adds approval mechanism for products.
template: feature-walkthrough-template
---

The *Product Approval Process* feature adds the approval mechanism for products by providing an optional `spy_product_abstract.approval_status` DB column to store product approval statuses. Thus, a shop owner can follow the review process and manage which products will be placed in the store by setting the corresponding approval statuses. The feature also provides the Back Office UI for managing the approval statuses and the corresponding Data importer.

## Related Developer documents

|INSTALLATION GUIDES  | DATA IMPORT |
|---------|---------|
| [Product Approval Process feature integration](/docs/pbc/all/product-information-management/{{page.version}}/install-and-upgrade/install-features/install-the-product-approval-process-feature.html) | [File details: product_abstract_approval_status.csv](/docs/pbc/all/product-information-management/{{page.version}}/import-and-export-data/products-data-import/file-details-product-abstract-approval-status.csv.html)  |
