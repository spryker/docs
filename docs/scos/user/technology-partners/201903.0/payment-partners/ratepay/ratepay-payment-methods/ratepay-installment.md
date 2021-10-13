---
title: RatePay - Installment
description: Integrate installment payment through Ratepay into the Spryker-based shop.
template: concept-topic-template
originalLink: https://documentation.spryker.com/v2/docs/ratepay-installment
originalArticleId: cde09fb6-93f1-4c5a-97b3-cb804e6e7b65
redirect_from:
  - /v2/docs/ratepay-installment
  - /v2/docs/en/ratepay-installment
related:
  - title: RatePay
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/ratepay.html
  - title: RatePay - Payment Workflow
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/technical-details-and-howtos/ratepay-payment-workflow.html
  - title: RatePay - Facade
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/technical-details-and-howtos/ratepay-facade.html
  - title: RatePay - How to Disable Address Updates from the Backend Application
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/technical-details-and-howtos/ratepay-how-to-disable-address-updates-from-the-backend-application.html
  - title: RatePay - Invoice
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/ratepay-payment-methods/ratepay-invoice.html
  - title: RatePay- Core Module Structure Diagram
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/ratepay-core-module-structure-diagram.html
  - title: RatePay - Prepayment
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/ratepay-payment-methods/ratepay-prepayment.html
  - title: RatePay - State Machine Commands and Conditions
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/technical-details-and-howtos/ratepay-state-machine-commands-and-conditions.html
  - title: RatePay - Direct Debit
    link: docs/scos/user/technology-partners/page.version/payment-partners/ratepay/ratepay-payment-methods/ratepay-direct-debit.html
---

The shop must implement the Calculation Request operation to calculate an example installment plan and show it to the customer. Some input parameters for the calculation are passed from the shop (e.g. the shopping basket total), others are stored in the merchant's RatePAY profile held by the Gateway (e.g. the allowed interest rate range). The merchant's profile parameters can be retrieved by the Configuration Request operation.

## Workflow Scenarios

### Payment Flow
![Click Me](https://spryker.s3.eu-central-1.amazonaws.com/docs/Technology+Partners/Payment+Partners/Ratepay/ratepay-installment-payment-flow.png) 

### Cancellation Flow
![Click Me](https://spryker.s3.eu-central-1.amazonaws.com/docs/Technology+Partners/Payment+Partners/Ratepay/ratepay-installment-cancellation-flow.png) 

### Partial Cancellation Flow
![Click Me](https://spryker.s3.eu-central-1.amazonaws.com/docs/Technology+Partners/Payment+Partners/Ratepay/ratepay-installment-partial-cancellation-flow.png) 

### Refund Flow
![Click Me](https://spryker.s3.eu-central-1.amazonaws.com/docs/Technology+Partners/Payment+Partners/Ratepay/ratepay-installment-refund-flow.png) 

## Integrating RatePAY Installment Payment

In order to integrate installment payment, two simple steps are needed: set RatePAY installment payment configuration and call the facade functions.

### Set RatePAY Installment Configuration

The installment requests use two additional types of requests called Configuration and Calculation Requests.

Three groups of configuration are defined:

* transaction configuration for handling the basic requests (init-payment, payment-request, etc)
* installment configuration for handling configuration
* calculation for handling calculation requests.

The configuration to integrate Installment payment method using RatePAY is:

* `PROFILE_ID`: merchant's login (required).
* `SECURITY_CODE`: merchant's password (required).
* `SHOP_ID`: shop identifier (required).
* `SYSTEM_ID`: system identifier (required).
* `CLIENT_VERSION`: client system version.
* `CLIENT_NAME`: client name.
* `RATEPAY_REQUEST_VERSION`: request version.
* R `ATEPAY_REQUEST_XMLNS_URN`: request XMLNS urn.
* `MODE`: the mode of the transaction, either test or live (required).
* `API_TEST_URL`: test mode API url.
* `API_LIVE_URL`: live mode API url.
* `DEBIT_PAY_TYPES`: debit pay types, can be DIRECT-DEBIT or BANK-TRANSFER.
* `INSTALLMENT_CALCULATION_TYPES`: installment calculator types, can be by time or by date.

You can copy over configs to your config from the RatePAY module's `config.dist.php` file.

### Perform Requests

In order to perform the needed requests, you can easily use the implemented state machine commands and conditions. The [RatePAY State Machine Commands and Conditions](/docs/scos/dev/technology-partners/201903.0/payment-partners/ratepay/ratepay-state-machine-commands-and-conditions.html) section gives a summary of them. You can also use the facade methods directly which, however, are invoked by the state machine.

