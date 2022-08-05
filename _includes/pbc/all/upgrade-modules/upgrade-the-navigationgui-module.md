

## Upgrading from version 1.* to version 2.*

In version 2, validity dates allow presetting date boundaries for each navigation node to control their own and their descendants visibility.

* Upgrade `Navigation` module to at least 2.0.0 version. See [Migration Guide - Navigation](/docs/scos/dev/module-migration-guides/migration-guide-navigation.html) to learn how to migrate the `Navigation` module.
* Update the `NavigationGui` module to at least 2.0.0 version in your `composer.json`.
* Make sure the new Zed user interface assets are built by running `npm run zed` (or `antelope build zed` for older versions).

Now, validity dates will be stored in Storage.

To apply validity dates on navigation node display, take a look on Navigation feature integration.
