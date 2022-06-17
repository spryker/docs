---
title: "HowTo: Import delivery methods linked to store"
description: Use the guide to learn how to import delivery methods assigned to specific stores in the Back Office.
last_updated: Jun 16, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/ht-import-delivery-methods-linked-to-store
originalArticleId: 45054e18-b4d1-44fa-bbca-f2478a52412d
redirect_from:
  - /2021080/docs/ht-import-delivery-methods-linked-to-store
  - /2021080/docs/en/ht-import-delivery-methods-linked-to-store
  - /docs/ht-import-delivery-methods-linked-to-store
  - /docs/en/ht-import-delivery-methods-linked-to-store
  - /v6/docs/ht-import-delivery-methods-linked-to-store
  - /v6/docs/en/ht-import-delivery-methods-linked-to-store
  - /v5/docs/ht-import-delivery-methods-linked-to-store
  - /v5/docs/en/ht-import-delivery-methods-linked-to-store
  - /v4/docs/ht-import-delivery-methods-linked-to-store
  - /v4/docs/en/ht-import-delivery-methods-linked-to-store
related:
  - title: Shipment feature overview
    link: docs/scos/user/features/shipment-feature-overview.html
  - title: Creating a Carrier Company
    link: docs/scos/user/back-office-user-guides/administration/delivery-methods/creating-carrier-companies.html
  - title: Creating and Managing Delivery Methods
    link: docs/scos/user/back-office-user-guides/administration/delivery-methods/creating-and-managing-delivery-methods.html
---

In addition to creating and managing delivery methods in the Back Office <!-- link -->, you can also import them with the stores assigned from a CSV file.

By default, the data is stored to the `/ShipmentDataImport/data/import/delivery_method_store.csv` file that should contain the following columns:

```yaml
shipment_method_key,store_name
```

where
* `shipment_method`: Name of the delivery method you want to create
* `store_name`: Store in which the delivery method are available

To import delivery methods linked to the stores from the `/ShipmentDataImport/data/import/delivery_method_store.csv` file, run the following console command:

```bash
console data:import:shipment-method-store
```

If successful, the imported data is added to the `spy_shipment_method_store` database table and appear on the list of delivery methods in the Back Office. For more information about how to view and update the delivery methods, see [Creating and managing delivery methods](/docs/scos/user/back-office-user-guides/administration/delivery-methods/creating-and-managing-delivery-methods.html) <!-- link -->.
