---
title: Queue data import feature integration
description: This guide will navigate you through the process of integrating the Queue Data feature in Spryker OS.
template: feature-integration-guide-template
originalLink: https://documentation.spryker.com/v6/docs/queue-data-import-feature-integration
originalArticleId: 3bd928dc-4bb6-43e9-b67c-83961d318fd1
redirect_from:
  - /v6/docs/queue-data-import-feature-integration
  - /v6/docs/en/queue-data-import-feature-integration
related:
  - title: Data import
    link: docs/scos/dev/sdk/page.version/data-import.html
---

## Install Feature Core

### 1)  Install the required modules using Composer

Run the following command to install the required modules:

```bash
composer require spryker/data-import:"1.5.0" spryker/data-import-extension:"1.1.0" --update-with-dependencies`
```
<section contenteditable="false" class="warningBox"><div class="content">

**Verification**
Make sure that the following modules have been installed:

| Module |Expected Directory  |
| --- | --- |
|`DataImport`  | `vendor/spryker/data-import` |
|  `DataImportExtension`| `vendor/spryker/data-import-extension` |
</div></section>

### 2) Set up Transfer Objects

Run the following command to generate transfer changes:

```bash
console transfer:generate`
```

<section contenteditable="false" class="warningBox"><div class="content">

**Verification**    
Make sure that the following changes have been applied in the transfer objects:

| Transfer | Type | Event | Path |
| --- | --- | --- | --- |
| `DataSetItem` | class | created | `src/Generated/Shared/Transfer/DataSetItemTransfer.php` |
| `QueueWriterConfiguration` | class | created | `src/Generated/Shared/Transfer/QueueWriterConfigurationTransfer.php` |
| `DataImporterQueueDataImporterConfiguration` | class | created | `src/Generated/Shared/Transfer/DataImporterQueueDataImporterConfigurationTransfer.php` |
| `DataImporterQueueReaderConfiguration` | class | created | `src/Generated/Shared/Transfer/DataImporterQueueReaderConfigurationTransfer.php` |
</div></section>
