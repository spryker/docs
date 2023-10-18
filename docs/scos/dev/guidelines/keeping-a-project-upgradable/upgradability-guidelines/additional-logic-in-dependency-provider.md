---
title: Additional logic in dependency provider
description: Reference information for evaluator tools.
template: howto-guide-template
redirect_from:
---

The *Additional logic in dependency provider* check checks the way plugins are registered in the dependency provider on the project level.

## Problem description

At the project level, developers use `if` structures with diverse expressions in dependency providers to selectively register plugins in specific cases.

The expressions utilized within the `if` statements should not overly complicate the logic within the dependency provider.
This check ensures that if an `if` structure is used for plugin registration, only one of the subsequent expressions is used:

1. `class_exists` function call

Usage of the `class_exists` function call inside of the `if` statement is allowed for BC reasons only.

Below is an example of the `class_exists` function call inside of the `if` statement:

```php
namespace Pyz\Zed\Form;

use Spryker\Zed\WebProfiler\Communication\Plugin\Form\WebProfilerFormPlugin;

class FormDependencyProvider extends SprykerFormDependencyProvider
{
    /**
     * @return array<\Spryker\Shared\FormExtension\Dependency\Plugin\FormPluginInterface>
     */
    protected function getFormPlugins(): array
    {
        $formPlugins = [];

        if (class_exists(WebProfilerFormPlugin::class)) {
            $formPlugins[] = new WebProfilerFormPlugin();
        }

        return $formPlugins;
    }
}
```

2. `isDevelopment` function call

The usage of `isDevelopment` checks is allowed in order to register the plugins that are needed in development mode only (e.g. profiling, debug, etc.).

```php
namespace Pyz\Zed\Console;

use Spryker\Zed\Console\ConsoleDependencyProvider as SprykerConsoleDependencyProvider;
use Spryker\Zed\Development\Communication\Console\CodeTestConsole;
use Spryker\Zed\Kernel\Container;

class ConsoleDependencyProvider extends SprykerConsoleDependencyProvider
{
    /**
     * @param \Spryker\Zed\Kernel\Container $container
     *
     * @return array<\Symfony\Component\Console\Command\Command>
     */
    protected function getConsoleCommands(Container $container): array
    {
        $commands = [];

        if ($this->getConfig()->isDevelopmentConsoleCommandsEnabled()) {
            $commands[] = new CodeTestConsole();
        }

        return $commands;
    }
}
```

## Example of an evaluator error message

```bash
======================
MULTIDIMENSIONAL ARRAY
======================

Message: The if ($alwaysTrue) {} condition statement is forbidden in DependencyProvider
Target:  {PATH_TO_PROJECT}/Pyz/Zed/Checkout/CheckoutDependencyProvider.php

```

## Example of code that causes an evaluator error

The method `getFormPlugins` in `FormDependencyProvider` contains unsupported expressions in the `if` construct `$alwaysAddPlugin`.

```php
namespace Pyz\Zed\Form;

use Spryker\Zed\WebProfiler\Communication\Plugin\Form\WebProfilerFormPlugin;

class FormDependencyProvider extends SprykerFormDependencyProvider
{
    /**
     * @return array<\Spryker\Shared\FormExtension\Dependency\Plugin\FormPluginInterface>
     */
    protected function getFormPlugins(): array
    {
        $formPlugins = [];
        $alwaysTrue = true;

        if ($alwaysTrue) {
            $formPlugins[] = new WebProfilerFormPlugin();
        }

        return $formPlugins;
    }
}
```

## Resole the error

1. Try to avoid the usage of conditions in the dependency providers.
2. Use only the supported expressions in the `if` construct.
