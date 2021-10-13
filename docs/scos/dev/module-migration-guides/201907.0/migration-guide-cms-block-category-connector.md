---
title: Migration Guide - CMS Block Category Connector
template: module-migration-guide-template
originalLink: https://documentation.spryker.com/v3/docs/mg-cms-block-category-connector
originalArticleId: 3190ed70-865f-44e8-9191-ef1d49c67b47
redirect_from:
  - /v3/docs/mg-cms-block-category-connector
  - /v3/docs/en/mg-cms-block-category-connector
related:
  - title: CMS Block
    link: docs/scos/user/back-office-user-guides/page.version/content/blocks/cms-block.html
---

## Upgrading from Version 1.* to Version 2.*
Due to introducing the CMS Block positioning and CMS Block templates for Category, the CMS Block Category Connector module now requires Category >=4.0.
The migration will contain the following steps:

1. New module installation
2. Deprecations migration
3. Database migration
4. Data migration

### 1. New Module Installation
Install a new module by adding the following into your composer.json: `"spryker/cms-block-category-connector": "^2.0.0"` and running the composer update.
Follow the installation instructions to enable all connector plugins: CMS Block Category Connector: Installation.

### 2. Deprecations Migration
Change usage of `\Spryker\Shared\CmsBlockCategoryConnector\CmsBlockCategoryConnectorConstants::RESOURCE_TYPE_CMS_BLOCK_CATEGORY_CONNECTOR` to `\Spryker\Shared\CmsBlockCategoryConnector\CmsBlockCategoryConnectorConfig::RESOURCE_TYPE_CMS_BLOCK_CATEGORY_CONNECTOR`

### 3. Database Migration
Run Propel migrations.  `vendor/bin/console propel:diff`, manual review is necessary for the generated migration file. `vendor/bin/console propel:migratevendor/bin/console propel:model:build`

### 4. Data Migration
Notice: You can skip this step if you don't have data in `spy_cms_block_category_connector` table.
We prepared a migration script to migrate relations to Category.
The script can be found in [Migration Guide - CMS Block Category Connector Console](/docs/scos/dev/module-migration-guides/{{page.version}}/migration-guide-cms-block-category-connector-migration-console.html).
Copy script to `src/Pyz/Zed/CmsBlockCategoryConnector/Communication/Console/CmsBlockCategoryPosition.php` and register it in `Pyz\Zed\Console\ConsoleDependencyProvider`.
Check that the script covers your `Category and CmsBlockCategoryConnector` configuration.


```php
<?php
namespace Pyz\Zed\Console;

class ConsoleDependencyProvider extends SprykerConsoleDependencyProvider
{
    public function getConsoleCommands(Container $container)
    {
        $commands = [
          ...
          CmsBlockCategoryPosition()
        ];

        ...
    }
}
?>
```

Run console script to migrate CMS Block - Category relations to the new structure: `vendor/bin/console cms-block-category-connector:migrate-position`
<!-- Last review date: Aug 30, 2017-- by Denis Turkov -->
