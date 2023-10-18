This document describes how to install the Data Exchange API.

Data Exchange API is a powerful tool that enables seamless interaction with databases. You can easily access data by sending requests to a dedicated API endpoint. It lets you retrieve, create, update, and manage data in a flexible and efficient manner.

## Install feature core

Follow the steps below to install the Data Exchange API core.

### Prerequisites

Install the required features:

| NAME | VERSION | INTEGRATION GUIDE |
| --- | --- | --- |
| Glue Backend Api Application | {{page.version}} | [Glue API - Glue Storefront and Backend API applications integration](/docs/scos/dev/migration-concepts/migrate-to-decoupled-glue-infrastructure/decoupled-glue-infrastructure-integrate-storefront-and-backend-glue-api-applications.html) |
| Glue Authentication | {{page.version}} | [Glue API - Authentication integration](/docs/scos/dev/migration-concepts/migrate-to-decoupled-glue-infrastructure/decoupled-glue-infrastructure-integrate-the-authentication.html) |

### Install the required modules

Install the required modules using Composer:

```bash
composer require spryker/dynamic-entity-backend-api:"^1.0.0" spryker/dynamic-entity-gui:"^1.0.0" --update-with-dependencies
```

{% info_block warningBox "Verification" %}

Make sure that the following modules have been installed:

| MODULE | EXPECTED DIRECTORY |
| --- | --- |
| DynamicEntity | vendor/spryker/dynamic-entity |
| DynamicEntityBackendApi | vendor/spryker/dynamic-entity-backend-api |
| DynamicEntityGui | vendor/spryker/dynamic-entity-gui |

{% endinfo_block %}

### Set up the configuration

1. Move the following commands into the `setup-glue` section after the `demodata` step:

**config/install/docker.yml**

```yaml
setup-glue:
    controller-cache-warmup:
        command: 'vendor/bin/glue glue-api:controller:cache:warm-up'

    api-generate-documentation:
        command: 'vendor/bin/glue api:generate:documentation'
```

2. By default, requests are sent to `/dynamic-entity/{entity-alias}`. To replace the `dynamic-entity` part of the endpoint, adjust `DynamicEntityBackendApiConfig`:

**src/Pyz/Glue/DynamicEntityBackendApi/DynamicEntityBackendApiConfig.php**

```php
<?php

namespace Pyz\Glue\DynamicEntityBackendApi;

use Spryker\Glue\DynamicEntityBackendApiDynamicEntityBackendApiConfig as SprykerDynamicEntityBackendApiConfig;

class DynamicEntityBackendApiConfig extends SprykerDynamicEntityBackendApiConfig
{
    /**
     * Specification:
     * - Returns a route prefix value for a dynamic entity.
     *
     * @api
     *
     * @return string
     */
    public function getRoutePrefix(): string
    {
        return 'your-route-prefix';
    }
}
```

3. Optional: The Data Exchange API provides a logging mechanism to capture important information about requests and thrown exceptions.
   Logging is enabled by default. To disable logging or change the path of the log file, adjust `DynamicEntityBackendApiConfig`:

**src/Pyz/Glue/DynamicEntityBackendApi/DynamicEntityBackendApiConfig.php**

```php
<?php

namespace Pyz\Glue\DynamicEntityBackendApi;

use Spryker\Glue\DynamicEntityBackendApiDynamicEntityBackendApiConfig as SprykerDynamicEntityBackendApiConfig;

class DynamicEntityBackendApiConfig extends SprykerDynamicEntityBackendApiConfig
{
    /**
     * Specification:
     * - Returns absolute file path for dynamic entities logs.
     *
     * @api
     *
     * @return string
     */
    public function getLogFilepath(): string
    {
        return 'your-log-filepath.log';
    }

    /**
     * Specification:
     * - Defines whether logging for dynamic entities is enabled.
     *
     * @api
     *
     * @return bool
     */
    public function isLoggingEnabled(): bool
    {
        return true;
    }
}
```

<a name="exclude-database-schemas-from-configuring"></a>

4. Optional: To exclude database schemas from configuring, define them as follows:

**src/Pyz/Zed/DynamicEntityGui/DynamicEntityGuiConfig.php**

```php
<?php

namespace Pyz\Zed\DynamicEntityGui;

use Spryker\Zed\DynamicEntityGuiConfig as SprykerDynamicEntityGuiConfig;

class DynamicEntityGuiConfig extends SprykerDynamicEntityGuiConfig
{
    /**
     * Specification:
     * - Returns a list of tables that should not be used for dynamic entity configuration.
     *
     * @api
     *
     * @return array<string>
     */
    public function getDisallowedTables(): array
    {
        return [
            'spy_dynamic_entity_configuration',
        ];
    }
}
```

### Configure Dynamic Data installation

1. Optional: To set the default configuration data, create a configuration file:

<details open><summary markdown='span'>src/Pyz/Zed/DynamicEntity/data/installer/configuration.json</summary>

```json
[
  {
      "tableName": "spy_country",
      "tableAlias": "countries",
      "isActive": true,
      "definition": {
        "identifier": "id_country",
        "fields": [
          {
            "fieldName": "id_country",
            "fieldVisibleName": "id_country",
            "isCreatable": true,
            "isEditable": true,
            "type": "integer",
            "validation": { "isRequired": false }
          },
          {
            "fieldName": "iso2_code",
            "fieldVisibleName": "iso2_code",
            "isCreatable": true,
            "isEditable": true,
            "type": "string",
            "validation": { "isRequired": true }
          },
          {
            "fieldName": "iso3_code",
            "fieldVisibleName": "iso3_code",
            "isCreatable": true,
            "isEditable": true,
            "type": "string",
            "validation": { "isRequired": false }
          },
          {
            "fieldName": "name",
            "fieldVisibleName": "name",
            "isCreatable": true,
            "isEditable": true,
            "type": "string",
            "validation": { "isRequired": false }
          },
          {
            "fieldName": "postal_code_mandatory",
            "fieldVisibleName": "postal_code_mandatory",
            "isCreatable": true,
            "isEditable": true,
            "type": "string",
            "validation": { "isRequired": false }
          },
          {
            "fieldName": "postal_code_regex",
            "fieldVisibleName": "postal_code_regex",
            "isCreatable": true,
            "isEditable": true,
            "type": "string",
            "validation": { "isRequired": false }
          }
        ]
      }
    }
]
```
</details>
2. Add the path to the configuration file, to `DynamicEntityConfig`:

**src/Pyz/Zed/DynamicEntity/DynamicEntityConfig.php**

```php
<?php

/**
 * This file is part of the Spryker Suite.
 * For full license information, please view the LICENSE file that was distributed with this source code.
 */

namespace Pyz\Zed\DynamicEntity;

use Spryker\Zed\DynamicEntity\DynamicEntityConfig as SprykerDynamicEntityConfig;

class DynamicEntityConfig extends SprykerDynamicEntityConfig
{
    /**
     * @var string
     */
    protected const CONFIGURATION_FILE_PATH = '%s/src/Pyz/Zed/DynamicEntity/data/installer/configuration.json';

    /**
     * @return string
     */
    public function getInstallerConfigurationDataFilePath(): string
    {
        return sprintf(static::CONFIGURATION_FILE_PATH, APPLICATION_ROOT_DIR);
    }
}
```

### Set up database schema and transfer objects

1. Apply database changes and generate entity and transfer changes:

```bash
console propel:install
console transfer:generate
```

{% info_block warningBox "Verification" %}

Make sure you've triggered the following changes by checking the database:

| DATABASE ENTITY | TYPE |
| --- | --- |
| spy_dynamic_entity_configuration | table |
| spy_dynamic_entity_configuration_relation | table |
| spy_dynamic_entity_configuration_relation_field_mapping | table |

Make sure the following transfers have been created:

| TRANSFER | TYPE | EVENT | PATH |
| --- | --- | --- | --- |
| ApiApplicationSchemaContext | class | created | src/Generated/Shared/Transfer/ApiApplicationSchemaContextTransfer.php |
| CriteriaRangeFilter | class | created | src/Generated/Shared/Transfer/CriteriaRangeFilterTransfer.php |
| DocumentationInvalidationVoterRequest | class | created | src/Generated/Shared/Transfer/DocumentationInvalidationVoterRequestTransfer.php |
| DynamicApiDefinition | class | created | src/Generated/Shared/Transfer/DynamicApiDefinitionTransfer.php |
| DynamicEntity | class | created | src/Generated/Shared/Transfer/DynamicEntityTransfer.php |
| DynamicEntityCollection | class | created | src/Generated/Shared/Transfer/DynamicEntityCollectionTransfer.php |
| DynamicEntityCollectionDeleteCriteria | class | created | src/Generated/Shared/Transfer/DynamicEntityCollectionDeleteCriteriaTransfer.php |
| DynamicEntityCollectionRequest | class | created | src/Generated/Shared/Transfer/DynamicEntityCollectionRequestTransfer.php |
| DynamicEntityCollectionResponse | class | created | src/Generated/Shared/Transfer/DynamicEntityCollectionResponseTransfer.php |
| DynamicEntityConfiguration | class | created | src/Generated/Shared/Transfer/DynamicEntityConfigurationTransfer.php |
| DynamicEntityConfigurationCollection | class | created | src/Generated/Shared/Transfer/DynamicEntityConfigurationCollectionTransfer.php |
| DynamicEntityConfigurationCollectionRequest | class | created | src/Generated/Shared/Transfer/DynamicEntityConfigurationCollectionRequestTransfer.php |
| DynamicEntityConfigurationCollectionResponse | class | created | src/Generated/Shared/Transfer/DynamicEntityConfigurationCollectionResponseTransfer.php |
| DynamicEntityConfigurationConditions | class | created | src/Generated/Shared/Transfer/DynamicEntityConfigurationConditionsTransfer.php |
| DynamicEntityConfigurationCriteria | class | created | src/Generated/Shared/Transfer/DynamicEntityConfigurationCriteriaTransfer.php |
| DynamicEntityConditions | class | created | src/Generated/Shared/Transfer/DynamicEntityConditionsTransfer.php |
| DynamicEntityCriteria | class | created | src/Generated/Shared/Transfer/DynamicEntityCriteriaTransfer.php |
| DynamicEntityDefinition | class | created | src/Generated/Shared/Transfer/DynamicEntityDefinitionTransfer.php |
| DynamicEntityFieldCondition | class | created | src/Generated/Shared/Transfer/DynamicEntityFieldConditionTransfer.php |
| DynamicEntityFieldDefinition | class | created | src/Generated/Shared/Transfer/DynamicEntityFieldDefinitionTransfer.php |
| DynamicEntityFieldValidation | class | created | src/Generated/Shared/Transfer/DynamicEntityFieldValidationTransfer.php |
| Error | class | created | src/Generated/Shared/Transfer/ErrorTransfer.php |
| ErrorCollection | class | created | src/Generated/Shared/Transfer/ErrorCollectionTransfer.php |
| GlueError | class | created | src/Generated/Shared/Transfer/GlueErrorTransfer.php |
| GlueFilter | class | created | src/Generated/Shared/Transfer/GlueFilterTransfer.php |
| GlueRequest | class | created | src/Generated/Shared/Transfer/GlueRequestTransfer.php |
| GlueResource | class | created | src/Generated/Shared/Transfer/GlueResourceTransfer.php |
| GlueResponse | class | created | src/Generated/Shared/Transfer/GlueResponseTransfer.php |
| Pagination | class | created | src/Generated/Shared/Transfer/PaginationTransfer.php |

Ensure successful generation of Propel entities by verifying that they exist. Additionally, modify the generated entity classes to extend from Spryker core classes.

| CLASS PATH | EXTENDS |
| --- | --- |
| src/Generated/Entity/SpyDynamicEntityConfiguration.php | \Spryker\Zed\DynamicEntity\Persistence\Propel\AbstractSpyDynamicEntityConfiguration |
| src/Generated/Entity/SpyDynamicEntityConfigurationQuery.php | \Spryker\Zed\DynamicEntity\Persistence\Propel\AbstractSpyDynamicEntityConfigurationQuery |
| src/Generated/Entity/SpyDynamicEntityConfigurationRelation.php | \Spryker\Zed\DynamicEntity\Persistence\Propel\AbstractSpyDynamicEntityConfigurationRelation |
| src/Generated/Entity/SpyDynamicEntityConfigurationRelationQuery.php | \Spryker\Zed\DynamicEntity\Persistence\Propel\AbstractSpyDynamicEntityConfigurationRelationQuery |
| src/Generated/Entity/SpyDynamicEntityConfigurationRelationFieldMapping.php | \Spryker\Zed\DynamicEntity\Persistence\Propel\AbstractSpyDynamicEntityConfigurationRelationFieldMapping |
| src/Generated/Entity/SpyDynamicEntityConfigurationRelationFieldMappingQuery.php | \Spryker\Zed\DynamicEntity\Persistence\Propel\AbstractSpyDynamicEntityConfigurationRelationFieldMappingQuery |


{% endinfo_block %}


### Add translations

1. Append the glossary according to your language configuration:

**src/data/import/glossary.csv**

```yaml
dynamic_entity.validation.invalid_data_format,"Invalid or missing data format. Please ensure that the data is provided in the correct format. Example request body: {'data':[{...},{...},..]}",en_US
dynamic_entity.validation.invalid_data_format,"Ungültiges oder fehlendes Datenformat. Stellen Sie bitte sicher, dass die Daten im richtigen Format bereitgestellt werden. Beispiel Anforderungskörper: {'data':[{...},{...}]}",de_DE
dynamic_entity.validation.persistence_failed,"Failed to persist the data. Please verify the provided data and try again.",en_US
dynamic_entity.validation.persistence_failed,"Das Speichern der Daten ist fehlgeschlagen. Bitte überprüfen Sie die bereitgestellten Daten und versuchen Sie es erneut.",de_DE
dynamic_entity.validation.persistence_failed_duplicate_entry,"Failed to persist the data. Please verify the provided data and try again. Entry is duplicated.",en_US
dynamic_entity.validation.persistence_failed_duplicate_entry,"Das Speichern der Daten ist fehlgeschlagen. Bitte überprüfen Sie die bereitgestellten Daten und versuchen Sie es erneut. Eintrag is doppelt vorhanden.",de_DE
dynamic_entity.validation.entity_does_not_exist,"The entity could not be found in the database.",en_US
dynamic_entity.validation.entity_does_not_exist,"Die Entität konnte in der Datenbank nicht gefunden werden.",de_DE
dynamic_entity.validation.invalid_field_type,"Invalid data type for field: %fieldName%",en_US
dynamic_entity.validation.invalid_field_type,"Ungültiger Datentyp: %fieldName%",de_DE
dynamic_entity.validation.invalid_field_value,"Invalid data value for field: %fieldName%, row number: %rowNumber%. Field rules: %validationRules%",en_US
dynamic_entity.validation.invalid_field_value,"Ungültiger Datenwert für das Feld: %fieldName%, Zeilennummer: %rowNumber%. Feldregeln: %validationRules%",de_DE
dynamic_entity.validation.required_field_is_missing,"The required field must not be empty. Field: '%fieldName%'",en_US
dynamic_entity.validation.required_field_is_missing,"Das erforderlich Feld darf nicht leer sein. Feld: '%fieldName%'",de_DE
dynamic_entity.validation.entity_not_found_or_identifier_is_not_creatable,"Entity `%identifier%` not found by identifier, and new identifier can not be persisted. Please update the request.",en_US
dynamic_entity.validation.entity_not_found_or_identifier_is_not_creatable,"Entität `%identifier%` konnte anhand der ID nicht gefunden werden, und die neue ID kann nicht dauerhaft gespeichert werden. Bitte aktualisieren Sie die Anfrage.",de_DE
dynamic_entity.validation.modification_of_immutable_field_prohibited,"Modification of immutable field `%fieldName%` is prohibited",en_US
dynamic_entity.validation.modification_of_immutable_field_prohibited,"Änderung des unveränderlichen Feldes %fieldName% ist nicht zulässig.",de_DE
dynamic_entity.validation.missing_identifier,"Incomplete Request - missing identifier",en_US
dynamic_entity.validation.missing_identifier,"Unvollständige Anforderung - fehlende ID",de_DE
```

2. Import data:

```bash
console data:import glossary
```

{% info_block warningBox "Verification" %}

Make sure the configured data has been added to the `spy_glossary` database table.

{% endinfo_block %}

### Configure navigation

1. Add the Dynamic Exchange API section to `navigation.xml`:

**config/Zed/navigation.xml**

```xml
<?xml version="1.0"?>
<config>
    <dynamic-entities-gui>
        <label>Data Exchange API Configuration</label>
        <title>Data Exchange API Configuration</title>
        <icon>fa-exchange-alt</icon>
        <bundle>dynamic-entity-gui</bundle>
        <controller>configuration-list</controller>
        <action>index</action>
        <pages>
            <dynamic-entity-create>
                <label>Create new configuration</label>
                <title>Create new configuration</title>
                <bundle>dynamic-entity-gui</bundle>
                <controller>configuration-create</controller>
                <action>index</action>
                <visible>0</visible>
            </dynamic-entity-create>
            <dynamic-entity-edit>
                <label>Edit configuration</label>
                <title>Edit configuration</title>
                <bundle>dynamic-entity-gui</bundle>
                <controller>configuration-edit</controller>
                <action>index</action>
                <visible>0</visible>
            </dynamic-entity-edit>
        </pages>
    </dynamic-entities-gui>
</config>
```


2. Update the navigation cache:

```bash
console navigation:build-cache
```

{% info_block warningBox "Verification" %}

Make sure the Data Exchange API section has been added to the Back Office navigation.

{% endinfo_block %}

### Set up behavior

Enable the following behaviors by registering the plugins:

| PLUGIN | SPECIFICATION | NAMESPACE |
| --- | --- | --- |
| PropelApplicationPlugin | Initializes `PropelOrm`. | Spryker\Zed\Propel\Communication\Plugin\Application |
| DynamicEntityApiSchemaContextExpanderPlugin | Adds dynamic entities to the documentation generation context. | Spryker\Glue\DynamicEntityBackendApi\Plugin\DocumentationGeneratorApi |
| DynamicEntityDocumentationInvalidationVoterPlugin | Checks if the dynamic entity configuration was changed within the provided interval. | Spryker\Glue\DynamicEntityBackendApi\Plugin\DocumentationGeneratorApi |
| DynamicEntityOpenApiSchemaFormatterPlugin | Formats dynamic entities of the Open API 3 schema: info, components, paths, tags. | Spryker\Glue\DynamicEntityBackendApi\Plugin\DocumentationGeneratorOpenApi |
| DynamicEntityRouteProviderPlugin | Adds routes for the provided dynamic entity to the RouteCollection. | Spryker\Glue\DynamicEntityBackendApi\Plugin |
| DynamicEntityProtectedPathCollectionExpanderPlugin | Expands the list of protected endpoints with dynamic entity endpoints. | Spryker\Glue\DynamicEntityBackendApi\Plugin\GlueBackendApiApplicationAuthorizationConnector |

<details open>
<summary markdown='span'>src/Pyz/Glue/Console/ConsoleDependencyProvider.php</summary>

```php
<?php

namespace Pyz\Glue\Console;

use Spryker\Glue\Console\ConsoleDependencyProvider as SprykerConsoleDependencyProvider;
use Spryker\Glue\Kernel\Container;
use Spryker\Zed\Propel\Communication\Plugin\Application\PropelApplicationPlugin;

class ConsoleDependencyProvider extends SprykerConsoleDependencyProvider
{
    /**
     * @param \Spryker\Glue\Kernel\Container $container
     *
     * @return array<\Spryker\Shared\ApplicationExtension\Dependency\Plugin\ApplicationPluginInterface>
     */
    public function getApplicationPlugins(Container $container): array
    {
        $applicationPlugins = parent::getApplicationPlugins($container);

        $applicationPlugins[] = new PropelApplicationPlugin();

        return $applicationPlugins;
    }
}
```
</details>

<details open>
<summary markdown='span'>src/Pyz/Glue/DocumentationGeneratorApi/DocumentationGeneratorApiDependencyProvider.php</summary>

```php
<?php

namespace Pyz\Glue\DocumentationGeneratorApi;

use Spryker\Glue\DocumentationGeneratorApi\DocumentationGeneratorApiDependencyProvider as SprykerDocumentationGeneratorApiDependencyProvider;
use Spryker\Glue\DocumentationGeneratorApi\Expander\ContextExpanderCollectionInterface;
use Spryker\Glue\DynamicEntityBackendApi\Plugin\DocumentationGeneratorApi\DynamicEntityApiSchemaContextExpanderPlugin;
use Spryker\Glue\DynamicEntityBackendApi\Plugin\DocumentationGeneratorApi\DynamicEntityDocumentationInvalidationVoterPlugin;

class DocumentationGeneratorApiDependencyProvider extends SprykerDocumentationGeneratorApiDependencyProvider
{
    /**
     * @var string
     */
    protected const GLUE_BACKEND_API_APPLICATION_NAME = 'backend';	    

    /**
     * @param \Spryker\Glue\DocumentationGeneratorApi\Expander\ContextExpanderCollectionInterface $contextExpanderCollection	     
     *	     
     * @return \Spryker\Glue\DocumentationGeneratorApi\Expander\ContextExpanderCollectionInterface	     
     */
    protected function getContextExpanderPlugins(ContextExpanderCollectionInterface $contextExpanderCollection): ContextExpanderCollectionInterface	    
    {	    
        $contextExpanderCollection->addExpander(new DynamicEntityApiSchemaContextExpanderPlugin(), [static::GLUE_BACKEND_API_APPLICATION_NAME]);
    }

    /**
     * @return array<\Spryker\Glue\DocumentationGeneratorApiExtension\Dependency\Plugin\DocumentationInvalidationVoterPluginInterface>
     */
    protected function getInvalidationVoterPlugins(): array
    {
        return [
            new DynamicEntityDocumentationInvalidationVoterPlugin(),
        ];
    }
}
```
</details>

{% info_block infoBox "" %}

The `DocumentationGeneratorApiDependencyProvider::getInvalidationVoterPlugins()` stack contains plugins that are used to invalidate the documentation cache.
If the documentation cache is not invalidated, the documentation will not be updated.

{% endinfo_block %}

<details open>
<summary markdown='span'>src/Pyz/Glue/DocumentationGeneratorOpenApi/DocumentationGeneratorOpenApiDependencyProvider.php</summary>

```php
<?php

namespace Pyz\Glue\DocumentationGeneratorOpenApi;

use Spryker\Glue\DocumentationGeneratorOpenApi\DocumentationGeneratorOpenApiDependencyProvider as SprykerDocumentationGeneratorOpenApiDependencyProvider;
use Spryker\Glue\DynamicEntityBackendApi\Plugin\DocumentationGeneratorOpenApi\DynamicEntityOpenApiSchemaFormatterPlugin;

class DocumentationGeneratorOpenApiDependencyProvider extends SprykerDocumentationGeneratorOpenApiDependencyProvider
{
    /**
     * @return array<\Spryker\Glue\DocumentationGeneratorOpenApiExtension\Dependency\Plugin\OpenApiSchemaFormatterPluginInterface>
     */
    protected function getOpenApiSchemaFormatterPlugins(): array
    {
        return [
            new DynamicEntityOpenApiSchemaFormatterPlugin(),
        ];
    }
}
```
</details>

<details open>
<summary markdown='span'>src/Pyz/Glue/GlueBackendApiApplication/GlueBackendApiApplicationDependencyProvider.php</summary>

```php
<?php

namespace Pyz\Glue\GlueBackendApiApplication;

use Spryker\Glue\DynamicEntityBackendApi\Plugin\DynamicEntityRouteProviderPlugin;
use Spryker\Glue\GlueBackendApiApplication\GlueBackendApiApplicationDependencyProvider as SprykerGlueBackendApiApplicationDependencyProvider;

class GlueBackendApiApplicationDependencyProvider extends SprykerGlueBackendApiApplicationDependencyProvider
{
    /**
     * @return array<\Spryker\Glue\GlueApplicationExtension\Dependency\Plugin\RouteProviderPluginInterface>	    
     */	    
    protected function getRouteProviderPlugins(): array	    
    {	    
        return [
            new DynamicEntityRouteProviderPlugin(),
        ];
    }	    
}
```
</details>

{% info_block warningBox "Verification" %}

Make sure you can operate data. For instructions, see [Requesting data using the Data Exchange API](/docs/scos/dev/glue-api-guides/{{page.version}}/data-exchange-api/how-to-guides/how-to-send-request-in-data-exchange-api.html)

{% endinfo_block %}

### Configure the scheduler

1. Adjust the scheduler project configuration:

**config/Zed/cronjobs/jenkins.php**

```php
$jobs[] = [
    'name' => 'glue-api-generate-documentation',
    'command' => '$PHP_BIN vendor/bin/glue api:generate:documentation --invalidated-after-interval 90sec',
    'schedule' => '*/1 * * * *',
    'enable' => true,
];
```

2. Apply the scheduler configuration update:

```bash
vendor/bin/console scheduler:suspend
vendor/bin/console scheduler:setup
vendor/bin/console scheduler:resume
```

{% info_block warningBox "Verification" %}

1. Configure at least one entity in `spy_dynamic_entity_configuration`. For instructions, see [How to configure Data Exchange API](/docs/scos/dev/glue-api-guides/{{page.version}}/data-exchange-api/how-to-guides/how-to-configure-data-exchange-api.html).
2. Make sure `src\Generated\GlueBackend\Specification\spryker_backend_api.schema.yml` has been generated and contains the corresponding endpoint with correct configurations.

{% endinfo_block %}
