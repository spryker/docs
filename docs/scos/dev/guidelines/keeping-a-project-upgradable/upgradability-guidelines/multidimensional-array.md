---
title: Multidimensional array
description: Reference information for evaluator tools.
template: howto-guide-template
redirect_from:
---

This check checks that project doesn't use the deeply nested multidimensional arrays in dependency providers, in order to not overload it with complicated logic.

## Problem description

If a plugins stack is used on the project level, not all structures are necessarily required. Deeply nested multidimensional arrays make configuration hard to upgrade.
This check verifies that multidimensional arrays have a maximum of two levels of nesting inside.

## Example of an evaluator error message

```bash
======================
MULTIDIMENSIONAL ARRAY
======================

Message: Reached max level of nesting for the plugin registration in the {FormDependencyProvider::getPlugins()}.
         The maximum allowed nesting level is 2. Refactor the code; otherwise, it can cause upgradability issues in the future.
Target:  Pyz\Yves\Module\ModuleDependencyProvider
```

## Example of code that causes an evaluator error

The methods `ModuleDependencyProvider` contains unsupported multidimensional arrays, which have more than two nesting levels inside.

```php
namespace Pyz\Yves\Module;

use Spryker\Yves\Module\ModuleDependencyProvider as SprykerModuleDependencyProvider;

class ModuleDependencyProvider extends SprykerModuleDependencyProvider
{
    ...
    protected function getPlugins(): array
    {
        return [ // 1st level
            GlossaryStorageConfig::PUBLISH_TRANSLATION => [ // 2nd level
                'delete' => [ // 3rd level. Only plugins registration should be on this nesting level
                    new GlossaryKeyDeletePublisherPlugin(),
                ],
                'write' => [
                    new GlossaryKeyWriterPublisherPlugin(),
                    new GlossaryTranslationWritePublisherPlugin(),
                ],
            ],
        ];
    }
}
```

## Resolving the error

Try to have simple configuration arrays. They shouldn't have more than two nesting levels inside.
