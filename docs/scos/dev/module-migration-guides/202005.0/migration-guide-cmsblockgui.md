---
title: Migration Guide - CmsBlockGui
description: Use the guide to update versions to the newer ones of the CMS Block GUI module.
template: module-migration-guide-template
originalLink: https://documentation.spryker.com/v5/docs/mg-cms-block-gui
originalArticleId: 5b52d3e6-d226-41d9-a969-2374133e23ba
redirect_from:
  - /v5/docs/mg-cms-block-gui
  - /v5/docs/en/mg-cms-block-gui
related:
  - title: Migration Guide - CMS Block
    link: docs/scos/dev/module-migration-guides/page.version/migration-guide-cmsblock.html
  - title: Migration Guide - CMS Block Collector
    link: docs/scos/dev/module-migration-guides/page.version/migration-guide-cms-block-collector.html
  - title: CMS Block
    link: docs/scos/user/back-office-user-guides/page.version/content/blocks/cms-block.html
---

## Upgrading from Version 1.* to Version 2.*

This version adds support to manage CMS Block-store relation through the dedicated CMS Block Administration Intrerface.

1. Installl/update `spryker/cms-block` to at least Version 2.0.0. For more information, see [Migration Guide - CMS Block](/docs/scos/dev/module-migration-guides/{{page.version}}/migration-guide-cmsblock.html).

2. Upgrade `spryker/cms-block-gui` to at least Version 2.0.0.

3. The CMS Block Back Office expects the CMS Block-store relation handling partial form to be defined in the dependency provider using the `Spryker\Zed\Kernel\Communication\Form\FormTypeInterface`. You can use the single store and multi-store compatible default implementation `Spryker\Zed\Store\Communication\Form\Type\StoreRelationToggleType` wrapped in `Spryker\Zed\Store\Communication\Plugin\Form\StoreRelationToggleFormTypePlugin`. Note: `Spryker\Zed\Store\Communication\Plugin\Form\StoreRelationToggleFormTypePlugin` is introduced in `spryker/store` version 1.2.0.

**Example injection:**
    
```php
<?php
namespace Pyz\Zed\CmsBlockGui;

use Spryker\Zed\CmsBlockGui\CmsBlockGuiDependencyProvider as CmsBlockGuiCmsBlockGuiDependencyProvider;
use Spryker\Zed\Store\Communication\Plugin\Form\StoreRelationToggleFormTypePlugin;

class CmsBlockGuiDependencyProvider extends CmsBlockGuiCmsBlockGuiDependencyProvider
{
    /**
     * @return \Spryker\Zed\Kernel\Communication\Form\FormTypeInterface
     */
    protected function createStoreRelationFormTypePlugin()
    {
        return new StoreRelationToggleFormTypePlugin();
    }
}
```

4. The following deprecated methods have been removed:
* `CmsBlockGuiCommunicationFactory::createCmsBlockForm()`
* `CmsBlockGuiCommunicationFactory::createCmsBlockGlossaryForm()`
* `CmsBlockGuiCommunicationFactory::createCmsBlockGlossaryPlaceholderTranslationFormType()`
* `CmsBlockGuiCommunicationFactory::createCmsBlockGlossaryPlaceholderFormType()`
* `CmsBlockForm::getName()`
* `CmsBlockGlossaryForm::getName()`
* `CmsBlockGlossaryPlaceholderForm::getName()`

5. Additionally these internal classes have changed. Take a look if you have customized any of them:
* `CmsBlockForm`
* `CmsBlockTable`
* `ViewBlockController`
* `ViewBlock/index.twig`

You can find more details for these changes on the [CMS Block GUI module release page](https://github.com/spryker/cms-block-gui/releases).

6. Go to a `CMS Block` edit page through the CMS Block Back Office to verify that the migration was successful. At this point the CMS Block-store relation configuration will be shown but being disabled if multi-store feature is not enabled yet. You can find additional information about multi-store CMS Block feature and the process of its enablement here.
