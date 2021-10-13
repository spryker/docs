---
title: RatePay - Facade
description: This article includes facade methods provided by Ratepay.
template: concept-topic-template
originalLink: https://documentation.spryker.com/v2/docs/ratepay-facade
originalArticleId: 44a2fd30-53f5-4f23-9b0e-5d9689d23346
redirect_from:
  - /v2/docs/ratepay-facade
  - /v2/docs/en/ratepay-facade
related:
  - title: RatePay
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/ratepay.html
  - title: RatePay - Payment Workflow
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/technical-details-and-howtos/ratepay-payment-workflow.html
  - title: RatePay - How to Disable Address Updates from the Backend Application
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/technical-details-and-howtos/ratepay-how-to-disable-address-updates-from-the-backend-application.html
  - title: RatePay - Invoice
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/ratepay-payment-methods/ratepay-invoice.html
  - title: RatePay- Core Module Structure Diagram
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/ratepay-core-module-structure-diagram.html
  - title: RatePay - Installment
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/ratepay-payment-methods/ratepay-installment.html
  - title: RatePay - Prepayment
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/ratepay-payment-methods/ratepay-prepayment.html
  - title: RatePay - State Machine Commands and Conditions
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/technical-details-and-howtos/ratepay-state-machine-commands-and-conditions.html
  - title: RatePay - Direct Debit
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/ratepay-payment-methods/ratepay-direct-debit.html
---

| Facade Method | Param | Return | Description |
| --- | --- | --- | --- |
| `saveOrderPayment` | `QuoteTransfer`, `CheckoutResponseTransfer` | void | Saves RatePAY payment method data according to quote and checkout response transfer data. |
| `initPayment` | `QuoteTransfer` | `RatepayResponseTransfer` | Performs the init payment request to RatePAY Gateway to retrieve transaction data. |
| `requestPayment` | `QuoteTransfer` | `RatepayResponseTransfer` | Performs check the customer and order details payment request to RatePAY Gateway. |
| `confirmPayment` | `OrderTransfer` | `RatepayResponseTransfer` | Performs the payment confirmation request to RatePAY Gateway. |
| `confirmDelivery` | `OrderTransfer`, array (Order Items) | `RatepayResponseTransfer` | Performs the delivery confirmation request to RatePAY Gateway. |
| `cancelPayment` | `OrderTransfer`, array (Order Items) | `RatepayResponseTransfer` | Performs the cancel payment request to RatePAY Gateway. |
| `refundPayment` | `OrderTransfer`, array (Order Items) | `RatepayResponseTransfer` | Performs the refund payment request to RatePAY Gateway. |
| `installmentConfiguration` | `QuoteTransfer` | `RatepayInstallmentConfigurationResponseTransfer` | Performs the installment payment method calculator configuration request to RatePAY Gateway. |
| `installmentCalculation` | `QuoteTransfer` | `RatepayInstallmentCalculationResponseTransfer` | Performs the installment payment method calculator calculation request to RatePAY Gateway. |
| `isPaymentConfirmed` | `OrderTransfer` | bool | Checks if the payment confirmation API request got success response from RatePAY Gateway. |
| `isDeliveryConfirmed` | `OrderTransfer` | bool | Checks if the delivery confirmation API request got success response from RatePAY Gateway. |
| `isRefundApproved` | `OrderTransfer` | bool | Checks if the payment refund API request got success response from RatePAY Gateway. |
| `isCancellationConfirmed` | `OrderTransfer` | bool | Checks if the payment cancellation API request got success response from RatePAY Gateway. |
| `requestProfile` |  | `RatepayProfileResponseTransfer` | Retrieves profile data from Ratepay Gateway. |
| `expandItems` | `CartChangeTransfer` | `CartChangeTransfer` | Expands cart items with necessary for RatePAY information (short_description, long_description, etc). |
| `install` | `MessengerInterface` | void | Installs module translations to project glossary. |
