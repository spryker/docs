---
title: Web Profiler Widget for Yves
description: This guide describes how to integrate and use the Web Profiler Widget available in Yves for development purposes.
template: howto-guide-template
originalLink: https://documentation.spryker.com/v5/docs/web-profiler-widget
originalArticleId: 90cc8f11-ab60-40bc-8462-a9b63e0af125
redirect_from:
  - /v5/docs/web-profiler-widget
  - /v5/docs/en/web-profiler-widget
related:
  - title: Web Profiler for Zed
    link: docs/scos/dev/migration-and-integration/page.version/development-tools/web-profiler-for-zed.html
---

{% info_block errorBox %}

The following guide only demonstrates how to enable a development tool.

{% endinfo_block %}

The _Web Profiler Widget_ provides a toolbar for debugging and informational purposes. The toolbar is located at the bottom of a loaded page.

The widget is based on _Symfony Profiler_. For details, see [Profiler documentation](https://symfony.com/doc/current/profiler.html).

## Modules

The following modules provide the profiler functionality:

*   **WebProfilerWidget** -`spryker-shop/web-profiler-widget`
*   **WebProfilerExtension** -`spryker/web-profiler-extension`

## Installation

Run the following command to install _WebProfilerWidget_ and the extension module:
```Bash
composer require spryker-shop/web-profiler-widget --dev
```
## Integration

To be able to use the _Web Profiler Widget_, add `\SprykerShop\Yves\WebProfilerWidget\Plugin\Application\WebProfilerApplicationPlugin`of the`spryker-shop/web-profiler-widget`module to `\Pyz\Yves\ShopApplication\ShopApplicationDependencyProvider::getApplicationPlugins()`.

## Configure WebProfilerWidget per Environment

The blow options can be used in the Router to configure _WebProfilerWidget_. The options are contained in `\SprykerShop\Shared\WebProfilerWidget\WebProfilerWidgetConstants`.

*   `\SprykerShop\Shared\WebProfilerWidget\WebProfilerWidgetConstants::IS_WEB_PROFILER_ENABLED`\- use this option to enable/disable _WebProfilerWidget_. By default, the widget is disabled.
*   `\SprykerShop\Shared\WebProfilerWidget\WebProfilerWidgetConstants::PROFILER_CACHE_DIRECTORY`\- use this option to specify the path where the _WebProfiler_ stores its cache.

## Extending WebProfilerWidget

You can extend _WebProfiler_ with the `\Spryker\Shared\WebProfilerExtension\Dependency\Plugin\WebProfilerDataCollectorPluginInterface` interface. It can be used for adding _Data Collectors_ to the profiler.

Individual _Data Collectors_ can be added to `\Pyz\Yves\WebProfilerWidget\WebProfilerWidgetDependencyProvider::getDataCollectorPlugins()`.

Spryker provides a lot of build-in collectors. You can locate them in `WebProfilerWidget/src/SprykerShop/Yves/WebProfilerWidget/Plugin/WebProfiler/`.
