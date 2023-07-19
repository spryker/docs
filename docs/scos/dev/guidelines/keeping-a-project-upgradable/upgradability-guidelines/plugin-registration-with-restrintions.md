---
title: Plugin registration with restrictions
description: Reference information for evaluator tools.
template: howto-guide-template
---

Some plugins have dependencies from other plugins and should be used only before or after another plugin. The *Plugin registration with restrictions* check checks that dependencies between the plugins are described according to the specification.

## Problem description

If plugins must be registered in a specific order, `after` and `before` annotations need to be provided in the documentation blocks before the plugin. They must also have specific syntax.

1. Annotation to register plugin before another one: 

```php
/**
* Restrictions:
* - before {@link <dependency_plugin_namespace>/<dependency_plugin_name>} <optional_description>
* - before {@link <dependency_plugin2_namespace>/<dependency_plugin2_name>} <optional_description>
*/
```

Below is an example of the annotation syntax needed to register a plugin before another one:

```php
    /**
    * Restrictions:
    * - before {@link \Spryker\Client\MerchantProductStorage\Plugin\ProductOfferStorage\MerchantProductProductOfferReferenceStrategyPlugin} Call it always before MerchantProductProductOfferReferenceStrategyPlugin.
    */
    new ProductOfferReferenceStrategyPlugin(),
```

Below is an example of the annotation syntax needed to register a plugin after another one:```

```php
/**
* Restrictions:
* - after {@link <dependency_plugin_namespace>/<dependency_plugin_name>} <optional_description>
* - after {@link <dependency_plugin2_namespace>/<dependency_plugin2_name>} <optional_description>
*/
```

Below is an example of the annotation syntax needed to register a plugin only after another one:```

```php
    /**
    * Restrictions:
    * - after {@link \Spryker\Client\ProductOfferStorage\Plugin\ProductOfferStorage\ProductOfferReferenceStrategyPlugin}
    * - after {@link \Spryker\Client\MerchantProductStorage\Plugin\ProductOfferStorage\MerchantProductProductOfferReferenceStrategyPlugin} Call it always after ProductOfferReferenceStrategyPlugin and MerchantProductProductOfferReferenceStrategyPlugin.
    */
    new DefaultProductOfferReferenceStrategyPlugin(),
```

## Example of an evaluator error message

```shell
==============================================
PLUGINS REGISTRATION WITH RESTRICTIONS CHECKER
==============================================

Message: Restriction rule does not match the pattern "/^\* - (before|after) \{@link (?<class>.+)\}( .*\.|)$/".
Target:  CategoryDependencyProvider.php
```

## Example of code that causes an evaluator error

```php
namespace Pyz\Zed\Category;

use Spryker\Zed\Category\CategoryDependencyProvider as SprykerDependencyProvider;

class CategoryDependencyProvider extends SprykerDependencyProvider
{
    protected function getProductOfferReferenceStrategyPlugins(): array
    {
        return [
            /**
              * Restrictions:
              * - Call it always before MerchantProductProductOfferReferenceStrategyPlugin.
              */
            new ProductOfferReferenceStrategyPlugin(),
            new MerchantProductProductOfferReferenceStrategyPlugin(),
        ];
    }
}
```

### Resolving the error

To solve this issue:

1. Rewrite the plugin restrictions annotation according to required format.
