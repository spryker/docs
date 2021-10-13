---
title: Amazon Pay - Refund
description: This article contain information on the refund process for the Amazon Pay module in Spryker.
template: concept-topic-template
originalLink: https://documentation.spryker.com/v3/docs/amazon-pay-refund-demoshop
originalArticleId: 24add898-e75b-4c97-9334-77918beb3f14
redirect_from:
  - /v3/docs/amazon-pay-refund-demoshop
  - /v3/docs/en/amazon-pay-refund-demoshop
related:
  - title: Amazon Pay - Obtaining an Amazon Order Reference and Information About Shipping Addresses
    link: docs/scos/user/technology-partners/page.version/payment-partners/amazon-pay/scos-integration/amazon-pay-obtaining-an-amazon-order-reference-and-information-about-shipping-addresses.html
  - title: Amazon Pay - Rendering a “Pay with Amazon” Button on the Cart Page
    link: docs/scos/user/technology-partners/page.version/payment-partners/amazon-pay/legacy-demoshop-integration/amazon-pay-rendering-a-pay-with-amazon-button-on-the-cart-page.html
  - title: Amazon Pay - Support of Bundled Products
    link: docs/scos/user/technology-partners/page.version/payment-partners/amazon-pay/legacy-demoshop-integration/amazon-pay-support-of-bundled-products.html
  - title: Amazon Pay - API
    link: docs/scos/user/technology-partners/page.version/payment-partners/amazon-pay/scos-integration/amazon-pay-api.html
  - title: Amazon Pay - Configuration for the SCOS
    link: docs/scos/user/technology-partners/page.version/payment-partners/amazon-pay/scos-integration/amazon-pay-configuration-for-the-scos.html
  - title: Amazon Pay - Sandbox Simulations
    link: docs/scos/user/technology-partners/page.version/payment-partners/amazon-pay/scos-integration/amazon-pay-sandbox-simulations.html
  - title: Amazon Pay - API
    link: docs/scos/user/technology-partners/page.version/payment-partners/amazon-pay/legacy-demoshop-integration/amazon-pay-api.html
  - title: Amazon Pay - Sandbox Simulations
    link: docs/scos/user/technology-partners/page.version/payment-partners/amazon-pay/legacy-demoshop-integration/amazon-pay-sandbox-simulations.html
  - title: Amazon Pay - Email Notifications
    link: docs/scos/user/technology-partners/page.version/payment-partners/amazon-pay/legacy-demoshop-integration/amazon-pay-email-notifications.html
  - title: Amazon Pay - Order Reference and Information about Shipping Addresses
    link: docs/scos/user/technology-partners/page.version/payment-partners/amazon-pay/legacy-demoshop-integration/amazon-pay-order-reference-and-information-about-shipping-addresses.html
---

After the successful authorization and capture processes, the order should be closed. This blocks any modifications to an order. From this state only Refund operation is possible. The refund can be partial if more than one item is set to refund or full.

Amazon only requires the amount of money which has to be refunded, and the calculation has to be implemented on the shop's side. Spryker OS provides a module for calculating the amount to refund. Regardless of the chosen setting, the refund is always asynchronous. Once requested, an order goes to "refund pending" status and then IPN notification will notify the shop if the refund was accepted or declined.
