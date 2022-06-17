---
title: Migration guide - Navigation
description: Use the guide to migrate to a newer version of the Navigation module.
last_updated: Jun 16, 2021
template: module-migration-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/mg-navigation
originalArticleId: 735f2654-395b-4da6-9b9d-fa878924105a
redirect_from:
  - /2021080/docs/mg-navigation
  - /2021080/docs/en/mg-navigation
  - /docs/mg-navigation
  - /docs/en/mg-navigation
  - /v1/docs/mg-navigation
  - /v1/docs/en/mg-navigation
  - /v2/docs/mg-navigation
  - /v2/docs/en/mg-navigation
  - /v3/docs/mg-navigation
  - /v3/docs/en/mg-navigation
  - /v4/docs/mg-navigation
  - /v4/docs/en/mg-navigation
  - /v5/docs/mg-navigation
  - /v5/docs/en/mg-navigation
  - /v6/docs/mg-navigation
  - /v6/docs/en/mg-navigation
  - /docs/scos/dev/module-migration-guides/migration-guide-navigation.html
related:
  - title: Migration guide - NavigationGui
    link: docs/scos/dev/module-migration-guides/migration-guide-navigationgui.html
---

## Upgrading from version 1.* to version 2.*

Version 2 adds validity date fields to navigation nodes to support `NavigationGui` module to control the temporal visibility of nodes.

* Update the `Navigation` module to at least  version 2.0.0 in your `composer.json`.
* Install the new database fields by running `vendor/bin/console propel:diff`. Propel should generate a migration file with the changes.
* Apply the database changes: `run vendor/bin/console propel:migrate`.
* Generate ORM models: `run vendor/bin/console propel:model:build`.
* Run `vendor/bin/console transfer:generate` to generate the new fields into the `Navigation` transfer object.

As a result:

* `valid_from` and `valid_to` fields are added to `spy_navigation_node` table.
* Corresponding properties, getters, and setters are added to `Navigation` transfer object.
