---
title: Heidelpay - Installation
description: This article contains installation information for the Heidelpay module into the Spryker Legacy Demoshop.
template: concept-topic-template
originalLink: https://documentation.spryker.com/v1/docs/heidelpay-installation
originalArticleId: 6209bf72-5ede-4287-883f-10c3f1822a53
redirect_from:
  - /v1/docs/heidelpay-installation
  - /v1/docs/en/heidelpay-installation
related:
  - title: Heidelpay
    link: docs/scos/user/technology-partners/page.version/payment-partners/heidelpay/heidelpay.html
  - title: Heidelpay - Integration into SCOS
    link: docs/scos/user/technology-partners/page.version/payment-partners/heidelpay/scos-integration/heidelpay-integration-into-scos.html
  - title: Heidelpay - Credit Card Secure
    link: docs/scos/user/technology-partners/page.version/payment-partners/heidelpay/heidelpay-payment-methods/heidelpay-credit-card-secure.html
  - title: Heidelpay - Configuration for SCOS
    link: docs/scos/user/technology-partners/page.version/payment-partners/heidelpay/scos-integration/heidelpay-configuration-for-scos.html
  - title: Heidelpay - Direct Debit
    link: docs/scos/user/technology-partners/page.version/payment-partners/heidelpay/heidelpay-payment-methods/heidelpay-direct-debit.html
  - title: Heidelpay - Paypal Authorize
    link: docs/scos/user/technology-partners/page.version/payment-partners/heidelpay/heidelpay-payment-methods/heidelpay-paypal-authorize.html
  - title: Heidelpay - Workflow for Errors
    link: docs/scos/user/technology-partners/page.version/payment-partners/heidelpay/technical-details-and-howtos/heidelpay-workflow-for-errors.html
  - title: Heidelpay - Integration into the Legacy Demoshop
    link: docs/scos/user/technology-partners/page.version/payment-partners/heidelpay/heidelpay-integration-into-the-legacy-demoshop.html
  - title: Heidelpay - Split-payment Marketplace
    link: docs/scos/user/technology-partners/page.version/payment-partners/heidelpay/heidelpay-payment-methods/heidelpay-split-payment-marketplace.html
  - title: Heidelpay - Easy Credit
    link: docs/scos/user/technology-partners/page.version/payment-partners/heidelpay/heidelpay-payment-methods/heidelpay-easy-credit.html
---

To install Heidelpay, if necessary, add  the Heidelpay repo to your repositories in composer.json:

 ```php
 "repositories": [
 ...
 {
 "type": "git",
 "url": "https://github.com/spryker-eco/Heidelpay.git"
 }
 ],
 ```

and run the following console command:
```php
composer require spryker-eco/heidelpay
```
