---
title: Migration Guide - ManualOrderEntryGui
description: Use the guide to migrate to a newer version of the ManualOrderEntryGui module.
template: module-migration-guide-template
originalLink: https://documentation.spryker.com/v6/docs/mg-manual-order-entry-gui
originalArticleId: 66c6d3e8-1aea-454b-9b08-c8dcf29fc9bd
redirect_from:
  - /v6/docs/mg-manual-order-entry-gui
  - /v6/docs/en/mg-manual-order-entry-gui
related:
  - title: Migration Guide - Shipment
    link: docs/scos/dev/module-migration-guides/page.version/migration-guide-shipment.html
---

## Upgrading from Version 0.8.* to Version 0.9.0

In the version 0.9.0 of the **ManualOrderEntryGui** module, we have added the ability to assign a delivery method to a store in the Back Office. You can find more details about the changes on the [ManualOrderEntryGui module](https://github.com/spryker/manual-order-entry-gui/releases) release page.

**To upgrade to the new version of the module, do the following:**

1. Upgrade the **ManualOrderEntryGui** module to the new version:

```bash
composer require spryker/manual-order-entry-gui: "^0.9.0" --update-with-dependencies
```
2. Generate the transfer objects:

```bash
console transfer:generate
```

*Estimated migration time: 5 min*

## Upgrading from Version 0.7.* to Version 0.8.0

In this new version of the **ManualOrderEntryGui** module, we have added support of split delivery. You can find more details about the changes on the [ManualOrderEntryGui module](https://github.com/spryker/manual-order-entry-gui/releases) release page.

{% info_block errorBox %}
This release is a part of the **Split delivery** concept migration. When you upgrade this module version, you should also update all other installed modules in your project to use the same concept as well as to avoid inconsistent behavior. For more information, see [Split Delivery Migration Concept](/docs/scos/dev/migration-concepts/split-delivery-migration-concept.html).
{% endinfo_block %}

**To upgrade to the new version of the module, do the following:**

1. Upgrade the **ManualOrderEntryGui** module to the new version:

```bash
composer require spryker/manual-order-entry-gui: "^0.8.0" --update-with-dependencies
```
2. Generate the transfer objects:

```bash
console transfer:generate
```

*Estimated migration time: 5 min*

## Upgrading from Version 0.5.* to Version 0.7.0

{% info_block infoBox %}
 In order to dismantle the Horizontal Barrier and enable partial module updates on projects, Technical Release took place. Public API of source and target major versions are equal. No migration efforts are required. Please [contact us](https://spryker.com/en/support/) if you have any questions.
{% endinfo_block %} if you have any questions. )
