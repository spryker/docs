

## Upgrading from version 4.* to version 6.0.0

{% info_block infoBox %}

In order to dismantle the Horizontal Barrier and enable partial module updates on projects, a Technical Release took place. Public API of source and target major versions are equal. No migration efforts are required. Please [contact us](https://spryker.com/en/support/) if you have any questions.

{% endinfo_block %}


## Upgrading from version 3.* to version 4.*

In version 4 we have added support for multi-currency. First of all make sure you have [migrated the Price module](/docs/scos/dev/module-migration-guides/migration-guide-price.html).
We have changed the way the default price type is assigned, it's not coming from the new price module, also the price will be assigned based on the current price mode, currency, type combination.
