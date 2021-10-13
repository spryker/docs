---
title: Migration Guide - CMS Collector
template: module-migration-guide-template
originalLink: https://documentation.spryker.com/v1/docs/mg-cms-collector
originalArticleId: a640d583-7de8-4e4a-a8d3-c17566a712ac
redirect_from:
  - /v1/docs/mg-cms-collector
  - /v1/docs/en/mg-cms-collector
related:
  - title: Migration Guide - CMS Block
    link: docs/scos/dev/module-migration-guides/page.version/migration-guide-cmsblock.html
---

## Upgrading from Version 1.* to Version 2.*
Upgrade `spryker/cms` module to at least 6.2 version. See [Migration Guide - CMS](/docs/scos/dev/module-migration-guides/{{page.version}}/migration-guide-cms.html) for more details.
Upgrade `spryker/cms-content-widget` module to at least 1.1 version if you use `CmsPageCollectorParameterMapExpanderPlugin` plugin.
CMS page data expander plugins are applied by the `spryker/cms` module instead of the `spryker/cms-collector` module:

* Amend your custom CMS page collector data expander plugins to use `CmsPageDataExpanderPluginInterface` plugin interface instead of the deprecated `CmsPageCollectorDataExpanderPluginInterface` plugin interface.
* If you use `CmsPageCollectorParameterMapExpanderPlugin` plugin, replace it with `CmsPageParameterMapExpanderPlugin` plugin.
* Register your CMS page data expander plugins to `spryker/cms` module in the `CmsDependencyProvider` dependency provider.

Example of CMS data expander plugin registration:

```php
<?php
namespace Pyz\Zed\Cms;

use Spryker\Zed\Cms\CmsDependencyProvider as SprykerCmsDependencyProvider;
use Spryker\Zed\CmsContentWidget\Communication\Plugin\CmsPageDataExpander\CmsPageParameterMapExpanderPlugin;

class CmsDependencyProvider extends SprykerCmsDependencyProvider
{
    /**
     * @return \Spryker\Zed\Cms\Dependency\Plugin\CmsPageDataExpanderPluginInterface[]
     */
    protected function getCmsPageDataExpanderPlugins()
    {
        return [
            new CmsPageParameterMapExpanderPlugin(),
        ];
    }
}
```

* Remove deprecated CMS page collector data expander plugin registrations from `spryker/cms-collector` module's dependency provider in `CmsCollectorDependencyProvider`.

<!-- Last review date: Sep. 22, 2017- by Karoly Gerner  -->
