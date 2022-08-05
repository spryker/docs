---
title: Implementing a query container
description: To create a new Query Container you can copy and paste the snippet from this article and replace Mymodule with your module name.
last_updated: Jun 16, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/implementing-a-query-container
originalArticleId: 6b16783d-1196-48ca-84ae-eeda50fd446e
redirect_from:
  - /2021080/docs/implementing-a-query-container
  - /2021080/docs/en/implementing-a-query-container
  - /docs/implementing-a-query-container
  - /docs/en/implementing-a-query-container
  - /v6/docs/implementing-a-query-container
  - /v6/docs/en/implementing-a-query-container
  - /v5/docs/implementing-a-query-container
  - /v5/docs/en/implementing-a-query-container
  - /v4/docs/implementing-a-query-container
  - /v4/docs/en/implementing-a-query-container
  - /v3/docs/implementing-a-query-container
  - /v3/docs/en/implementing-a-query-container
  - /v2/docs/implementing-a-query-container
  - /v2/docs/en/implementing-a-query-container
  - /v1/docs/implementing-a-query-container
  - /v1/docs/en/implementing-a-query-container
related: 
  - title: About the query container
    link: docs/scos/dev/back-end-development/zed/persistence-layer/query-container/query-container.html
  - title: Using a query container
    link: docs/scos/dev/back-end-development/zed/persistence-layer/query-container/using-a-query-container.html
---

{% info_block infoBox "When to use query containers" %}

Don't use query containers to cross module boundaries, as this increases modules coupling. However, you can use them behind [Repository](/docs/scos/dev/back-end-development/zed/persistence-layer/repository.html) and [Entity Manager](/docs/scos/dev/back-end-development/zed/persistence-layer/entity-manager.html) as query aggregations.
Previously, query containers were used to cross module borders (via dependency providers), which led to higher module coupling and leaking of persistence layer from one domain object to another, and therefore, to higher maintenance efforts and lower code reusability. This approach has been deprecated now, so we don't recommend using query containers like this in your project development.

{% endinfo_block %}

To create a new Query Container you can copy and paste the following snippet and replace `MyBundle` with your module name.

```php
<?php
namespace Pyz\Zed\MyBundle\Persistence;

use Spryker\Zed\Kernel\Persistence\AbstractQueryContainer;

/**
 * @method MyBundlePersistenceFactory getFactory()
 */
class MyBundleQueryContainer extends AbstractQueryContainer implements MyBundleQueryContainerInterface
{
}
```

## Conventions for query containers

There are some conventions which should be followed here:

* All methods have the prefix `query*()`.
* All public methods are exposed in the related interface (e.g. `MyBundleQueryContainerInterface`).
* Queries are returned unterminated, so that the user can add restrictions (limit, offset) and can choose how to terminate (`count()`, `find()`, `findAll()`).
* Query containers do not access higher layers. So no usage of a facade here.
* Query containers do not contain any logic which is not needed to build queries.

