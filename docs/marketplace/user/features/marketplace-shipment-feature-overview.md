---
title: Marketplace Shipment feature overview
description: This document contains concept information for the Marketplace Shipment feature.
template: concept-topic-template
---

The *Marketplace Shipment* feature allows splitting the [marketplace order](/docs/marketplace/user/features/{{page.version}}/marketplace-order-management-feature-overview/marketplace-order-management-feature-overview.html) into different shipments based on merchants who will process them.

A *shipment* is a set of two or more products combined by the same delivery address.

With the Marketplace Shipment feature, every merchant can define delivery price and expected delivery time, tax sets, and availability of the delivery method per store. Thus, a [marketplace order](/docs/marketplace/user/features/{{page.version}}/marketplace-order-management-feature-overview/marketplace-order-overview.html) has multiple delivery methods from different merchants.

## Marketplace Shipment on the Storefront

In the *Address* checkout step, buyers can define a common delivery address where all the shipments are to be delivered.
Then, in the *Shipment* checkout step, buyers can see that the products are grouped by a merchant into different shipments  by default. For each shipment, they can select a shipping method and a delivery date (optional).

![img](https://spryker.s3.eu-central-1.amazonaws.com/docs/Marketplace/user+guides/Features/Marketplace+Shipment/shipment-to-single-address.png)

Alternatively, buyers can use the **Deliver to multiple addresses** drop-down option to assign a delivery address per cart item. By doing that, even items from the same merchant have separate shipments.

![img](https://spryker.s3.eu-central-1.amazonaws.com/docs/Marketplace/user+guides/Features/Marketplace+Shipment/deliver-shipment.png)


## Marketplace Shipment in the Back Office

In the Back Office, the shipments are displayed in the **Order Items** section on the **View Order: _[Order ID]_** page. A Marketplace administrator can view them.

![img](https://spryker.s3.eu-central-1.amazonaws.com/docs/Marketplace/user+guides/Features/Marketplace+Shipment/shipments-back-office.png)

## Marketplace Shipment in the Merchant Portal

On the **Order _[Order ID]_** drawer, every merchant can view only the shipment of their product offers and products.

![img](https://spryker.s3.eu-central-1.amazonaws.com/docs/Marketplace/user+guides/Features/Marketplace+Shipment/shipment-merchant-portal.png)

{% info_block warningBox "Developer guides" %}

Are you a developer? See [Marketplace Shipment feature walkthrough](/docs/marketplace/dev/feature-walkthroughs/{{page.version}}/marketplace-shipment-feature-walkthrough.html) for developers.

{% endinfo_block %}
