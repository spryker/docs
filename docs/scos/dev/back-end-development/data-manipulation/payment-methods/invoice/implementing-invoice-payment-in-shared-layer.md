---
title: Implementing Invoice payment in shared layer
description: This procedure will help us to identify the new payment type through some unique constants.
last_updated: Jun 16, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/ht-invoice-payment-fe-be-shared
originalArticleId: ddb4c3f0-4ea8-4cda-82a2-0ffd4fecac99
redirect_from:
  - /2021080/docs/ht-invoice-payment-fe-be-shared
  - /2021080/docs/en/ht-invoice-payment-fe-be-shared
  - /docs/ht-invoice-payment-fe-be-shared
  - /docs/en/ht-invoice-payment-fe-be-shared
  - /v6/docs/ht-invoice-payment-fe-be-shared
  - /v6/docs/en/ht-invoice-payment-fe-be-shared
  - /v5/docs/ht-invoice-payment-fe-be-shared
  - /v5/docs/en/ht-invoice-payment-fe-be-shared
  - /v4/docs/ht-invoice-payment-fe-be-shared
  - /v4/docs/en/ht-invoice-payment-fe-be-shared
  - /v3/docs/ht-invoice-payment-fe-be-shared
  - /v3/docs/en/ht-invoice-payment-fe-be-shared
  - /v2/docs/ht-invoice-payment-fe-be-shared
  - /v2/docs/en/ht-invoice-payment-fe-be-shared
  - /v1/docs/ht-invoice-payment-fe-be-shared
  - /v1/docs/en/ht-invoice-payment-fe-be-shared
related:
  - title: Implementing Invoice payment
    link: docs/scos/dev/back-end-development/data-manipulation/payment-methods/invoice/implementing-invoice-payment.html
  - title: Implementing Invoice payment in front end
    link: docs/scos/dev/back-end-development/data-manipulation/payment-methods/invoice/implementing-invoice-payment-in-front-end.html
  - title: Implementing Invoice payment in back end
    link: docs/scos/dev/back-end-development/data-manipulation/payment-methods/invoice/implementing-invoice-payment-in-back-end.html
  - title: Integrating Invoice payment into checkout
    link: docs/scos/dev/back-end-development/data-manipulation/payment-methods/invoice/integrating-invoice-payment-into-checkout.html
  - title: Testing the Invoice payment implementation
    link: docs/scos/dev/back-end-development/data-manipulation/payment-methods/invoice/testing-the-invoice-payment-implementation.html
---

This procedure will help us to identify the new payment type through some unique constants. We are going to define those constants under the `Shared` namespace, since they’re needed both by Yves and Zed.

1. Create the `PaymentMethodsConstants` interface under the `Shared` namespace, where you’ll define these unique constants.

<details open>
<summary markdown='span'>Code sample:</summary>

```php
<?php

namespace Pyz\Shared\PaymentMethods;

interface PaymentMethodsConstants
{

    /**
     * @const string
     */
    const PROVIDER = 'paymentmethods';

    /**
     * @const string
     */
    const PAYMENT_METHOD_INVOICE = 'invoice';

    /**
     * @const string
     */
    const PAYMENT_INVOICE_FORM_PROPERTY_PATH = static::PROVIDER . static::PAYMENT_METHOD_INVOICE;

}
```
</details>

1. Enrich the `Payment` transfer file with a new property that corresponds to the new payment method. Add `Shared/PaymentMethods/Transfer/invoicepayment.transfer.xml` file with the following content:

<details open>
<summary markdown='span'>Code sample:</summary>

```xml
<?xml version="1.0"?>
<transfers xmlns="spryker:transfer-01"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="spryker:transfer-01 http://static.spryker.com/transfer-01.xsd">

    <transfer name="Payment">
        <!-- Should be equal to PaymentMethodsConstants::PAYMENT_INVOICE_FORM_PROPERTY_PATH.
		Then the form fields can be automatically mapped to the transfer object inside this field. -->
        <property name="paymentmethodsinvoice" type="string"/>
    </transfer>
    </transfers>
```
</details>

3. Run the `vendor/bin/console transfer:generate` command to have the `PaymentTransfer` class updated.
