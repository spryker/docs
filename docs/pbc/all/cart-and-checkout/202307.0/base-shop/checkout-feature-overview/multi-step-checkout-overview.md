---
title: Multi-step checkout overview
description: The checkout is based on a flexible step engine and can be adjusted to any use case.
last_updated: Jun 23, 2021
template: concept-topic-template
originalLink: https://documentation.spryker.com/2021080/docs/multi-step-checkout
originalArticleId: 05845681-637c-46cd-84f7-d548a089d2a6
redirect_from:
  - /2021080/docs/multi-step-checkout
  - /2021080/docs/en/multi-step-checkout
  - /docs/multi-step-checkout
  - /docs/en/multi-step-checkout
  - /docs/scos/user/features/201811.0/checkout-feature-overview/multi-step-checkout-overview.html
  - /docs/scos/user/features/202200.0/checkout-feature-overview/multi-step-checkout-overview.html
  - /docs/scos/user/features/202307.0/checkout-feature-overview/multi-step-checkout-overview.html
  - /docs/pbc/all/cart-and-checkout/checkout-feature-overview/multi-step-checkout-overview.html  
  - /docs/pbc/all/cart-and-checkout/202307.0/checkout-feature-overview/multi-step-checkout-overview.html  
---

The checkout workflow is a fully customizable multi-step process. The standard steps include customer registration and login, shipping and billing address, shipment method and costs, payment method, checkout overview, and checkout success.

Using the Spryker step engine, you can design different checkout types, such as a one-page checkout or an invoice page replacing the payment page. The step engine enables the following functions:

* Checkout as the guest, registered customer, or register in the checkout flow.
* Hooks for integrating payment or shipment methods.
* Progress bar to navigate between checkout steps.

The following example shows how the checkout works in the Spryker Demo Shop for a guest user:

![image](https://spryker.s3.eu-central-1.amazonaws.com/docs/Features/Checkout/Multi-Step+Checkout/shop-guide-checkout.gif)
