---
title: Migration Guide - Catalog
template: module-migration-guide-template
originalLink: https://documentation.spryker.com/v2/docs/mg-catalog
originalArticleId: 49ac9138-85f5-430e-af89-cbceb3d9566e
redirect_from:
  - /v2/docs/mg-catalog
  - /v2/docs/en/mg-catalog
related:
  - title: Migration Guide - Category
    link: docs/scos/dev/module-migration-guides/page.version/migration-guide-category.html
---

## Upgrading from Version 3.* to Version 4.*

Due to introducing the Suggestion Search feature, the Catalog bundle now requires Search >=5.2.
To upgrade from 3.* to 4.\*:
1. Before upgrading to the new version, make sure that you do not use any deprecated code from version 3.\*. Check the description of the deprecated code to see what you will need to use instead.
2. In the previous version `\Spryker\Client\Catalog\CatalogDependencyProvider` provided by default a stack of query expander and a stack of result formatter plugins for the `\Spryker\Client\Catalog\CatalogClient::catalogSearch()` method. In the new version you need to provide the necessary plugins from project level instead in: `\Pyz\Client\Catalog\CatalogDependencyProvider`.
