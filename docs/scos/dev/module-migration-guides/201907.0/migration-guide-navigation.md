---
title: Migration Guide - Navigation
template: module-migration-guide-template
originalLink: https://documentation.spryker.com/v3/docs/mg-navigation
originalArticleId: 3e61282c-882b-49f9-a839-87c8e51a61dc
redirect_from:
  - /v3/docs/mg-navigation
  - /v3/docs/en/mg-navigation
related:
  - title: Migration Guide - NavigationGui
    link: docs/scos/dev/module-migration-guides/page.version/migration-guide-navigationgui.html
---

## Upgrading from Version 1.* to Version 2.*

Version 2 adds validity date fields to navigation nodes to support NavigationGui module to control the temporal visibility of nodes.

* Update the Navigation module to at least  version 2.0.0 in your `composer.json`.
* Install the new database fields by running `vendor/bin/console propel:diff`. Propel should generate a migration file with the changes.
* Apply the database changes: `run vendor/bin/console propel:migrate`.
* Generate ORM models: `run vendor/bin/console propel:model:build`.
* Run `vendor/bin/console transfer:generate` to generate the new fields into the `Navigation` transfer object.

As a result

* `valid_from` and `valid_to` fields are added to `spy_navigation_node` table.
* Corresponding properties, getters, and setters are added to `Navigation` transfer object.

<!-- Last review date: Sep 21, 2017 by Karoly Gerner -->
