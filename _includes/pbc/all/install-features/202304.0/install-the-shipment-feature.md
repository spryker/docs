


{% info_block errorBox %}

The following feature integration guide expects the basic feature to be in place.<br>The current feature integration
guide only adds the following functionalities:

* Shipment Back Office UI
* Delivery method per store
* Shipment data import
* Sales order item extension

{% endinfo_block %}

## Install feature core

Follow the steps below to install the Shipment feature core.

### Prerequisites

To start the feature integration, integrate the required features:


| NAME         | VERSION          | INTEGRATION GUIDE                                                                                                                    |
|--------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| Spryker Core | {{site.version}} | [Spryker Core feature integration](/docs/scos/dev/feature-integration-guides/{{site.version}}/spryker-core-feature-integration.html) |  |

### 1) Install the required modules using Composer

```bash
composer require spryker-feature/shipment:"{{site.version}}" --update-with-dependencies
```

{% info_block warningBox "Verification" %}

Make sure that the following modules have been installed:

| MODULE                 | EXPECTED DIRECTORY                       |
|------------------------|------------------------------------------|
| ShipmentDataImport     | vendor/spryker/shipment-data-import      |
| ShipmentGui            | vendor/spryker/shipment-gui              |
| Shipment               | vendor/spryker/shipment                  |
| ShipmentType           | vendor/spryker/shipment-type             |
| ShipmentTypeDataImport | vendor/spryker/shipment-type-data-import |

{% endinfo_block %}

### 2) Set up database schema and transfer objects

Apply database changes and generate entity and transfer changes:

```bash
console propel:install
console transfer:generate
```

{% info_block warningBox "Verification" %}

Make sure that the following changes have been applied by checking your database:

| DATABASE ENTITY                      | TYPE   | EVENT   |
|--------------------------------------|--------|---------|
| spy_shipment_method_store            | table  | created |
| spy_shipment_type                    | table  | created |
| spy_shipment_type_store              | table  | created |
| spy_shipment_method.fk_shipment_type | column | created |

Make sure that the following changes have been applied in transfer objects:

| TRANSFER                                | TYPE     | EVENT   | PATH                                                                  |
|-----------------------------------------|----------|---------|-----------------------------------------------------------------------|
| ShipmentTransfer                        | class    | created | src/Generated/Shared/Transfer/ShipmentTransfer                        |
| StoreTransfer                           | class    | created | src/Generated/Shared/Transfer/StoreTransfer                           |
| DataImporterConfigurationTransfer       | class    | created | src/Generated/Shared/Transfer/DataImporterConfigurationTransfer       |
| DataImporterReaderConfigurationTransfer | class    | created | src/Generated/Shared/Transfer/DataImporterReaderConfigurationTransfer |
| DataImporterReportTransfer              | class    | created | src/Generated/Shared/Transfer/DataImporterReportTransfer              |
| DataImporterReportMessageTransfer       | class    | created | src/Generated/Shared/Transfer/DataImporterReportMessageTransfer       |
| TotalsTransfer                          | class    | created | src/Generated/Shared/Transfer/TotalsTransfer                          |
| ShipmentTypeCollectionTransfer          | class    | created | src/Generated/Shared/Transfer/ShipmentTypeCollectionTransfer          |
| ShipmentTypeTransfer                    | class    | created | src/Generated/Shared/Transfer/ShipmentTypeTransfer                    |
| ShipmentTypeCriteriaTransfer            | class    | created | src/Generated/Shared/Transfer/ShipmentTypeCriteriaTransfer            |
| ShipmentTypeConditionsTransfer          | class    | created | src/Generated/Shared/Transfer/ShipmentTypeConditionsTransfer          |
| ShipmentMethodTransfer.shipmentType     | property | created | src/Generated/Shared/Transfer/ShipmentMethodTransfer                  |

{% endinfo_block %}

### 3) Import shipment methods

{% info_block infoBox "Info" %}

The following imported entities are used as shipment methods in Spryker OS.

{% endinfo_block %}

1. Prepare your data according to your requirements using our demo data:

**vendor/spryker/spryker/Bundles/ShipmentDataImport/data/import/shipment.csv**
```yaml
shipment_method_key,name,carrier,taxSetName
spryker_dummy_shipment-standard,Standard,Spryker Dummy Shipment,Shipment Taxes
spryker_dummy_shipment-express,Express,Spryker Dummy Shipment,Shipment Taxes
spryker_drone_shipment-air_standard,Air Standard,Spryker Drone Shipment,Shipment Taxes
spryker_drone_shipment-air_sonic,Air Sonic,Spryker Drone Shipment,Shipment Taxes
spryker_drone_shipment-air_light,Air Light,Spryker Drone Shipment,Shipment Taxes
spryker_no_shipment,NoShipment,NoShipment,Tax Exempt
free_pickup,Free Pickup,pickup,Tax Exempt
```

| COLUMN              | REQUIRED? | DATA TYPE | DATA EXAMPLE                    | DATA EXPLANATION              |
|---------------------|-----------|-----------|---------------------------------|-------------------------------|
| shipment_method_key | mandatory | string    | spryker_dummy_shipment-standard | Key of the shipment method.   |
| name                | mandatory | string    | Standard                        | Name of the shipment method.  |
| carrier             | mandatory | string    | Spryker Dummy Shipment          | Name of the shipment carrier. |
| taxSetName          | mandatory | string    | Shipment Taxes                  | Tax set name.                 |

**vendor/spryker/spryker/Bundles/ShipmentDataImport/data/import/shipment_method_store.csv**
```yaml
shipment_method_key,store
spryker_dummy_shipment-standard,AT
spryker_dummy_shipment-standard,DE
spryker_dummy_shipment-standard,US
spryker_dummy_shipment-express,AT
spryker_dummy_shipment-express,DE
spryker_dummy_shipment-express,US
spryker_drone_shipment-air_standard,AT
spryker_drone_shipment-air_standard,DE
spryker_drone_shipment-air_standard,US
spryker_drone_shipment-air_sonic,AT
spryker_drone_shipment-air_sonic,DE
spryker_drone_shipment-air_sonic,US
spryker_drone_shipment-air_light,AT
spryker_drone_shipment-air_light,DE
spryker_drone_shipment-air_light,US
spryker_no_shipment,AT
spryker_no_shipment,DE
spryker_no_shipment,US
```

| COLUMN              | REQUIRED? | DATA TYPE | DATA EXAMPLE                    | DATA EXPLANATION                    |
|---------------------|-----------|-----------|---------------------------------|-------------------------------------|
| shipment_method_key | mandatory | string    | spryker_dummy_shipment-standard | Key of an existing shipping method. |
| store               | mandatory | string    | DE                              | Name of an existing store.          |

**vendor/spryker/spryker/Bundles/ShipmentDataImport/data/import/shipment_price.csv**
```yaml
shipment_method_key,store,currency,value_net,value_gross
spryker_dummy_shipment-standard,AT,EUR,290,390
spryker_dummy_shipment-express,AT,EUR,390,490
spryker_drone_shipment-air_standard,AT,EUR,350,400
spryker_drone_shipment-air_sonic,AT,EUR,700,900
spryker_drone_shipment-air_light,AT,EUR,1100,1200
spryker_dummy_shipment-standard,AT,CHF,350,460
spryker_dummy_shipment-express,AT,CHF,460,580
spryker_drone_shipment-air_standard,AT,CHF,420,480
spryker_drone_shipment-air_sonic,AT,CHF,720,1100
spryker_drone_shipment-air_light,AT,CHF,1300,1600
spryker_no_shipment,AT,EUR,0,0
spryker_no_shipment,AT,CHF,0,0
free_pickup,AT,EUR,,0
free_pickup,AT,CHF,,0
spryker_dummy_shipment-standard,DE,EUR,390,490
spryker_dummy_shipment-express,DE,EUR,490,590
spryker_drone_shipment-air_standard,DE,EUR,450,500
spryker_drone_shipment-air_sonic,DE,EUR,800,1000
spryker_drone_shipment-air_light,DE,EUR,1200,1500
spryker_dummy_shipment-standard,DE,CHF,450,560
spryker_dummy_shipment-express,DE,CHF,560,680
spryker_drone_shipment-air_standard,DE,CHF,520,580
spryker_drone_shipment-air_sonic,DE,CHF,920,1200
spryker_drone_shipment-air_light,DE,CHF,1400,1700
spryker_no_shipment,DE,EUR,0,0
spryker_no_shipment,DE,CHF,0,0
free_pickup,DE,EUR,,0
free_pickup,DE,CHF,,0
spryker_dummy_shipment-standard,US,EUR,390,490
spryker_dummy_shipment-express,US,EUR,490,590
spryker_drone_shipment-air_standard,US,EUR,450,500
spryker_drone_shipment-air_sonic,US,EUR,800,1000
spryker_drone_shipment-air_light,US,EUR,1200,1500
spryker_dummy_shipment-standard,US,CHF,450,560
spryker_dummy_shipment-express,US,CHF,560,680
spryker_drone_shipment-air_standard,US,CHF,520,580
spryker_drone_shipment-air_sonic,US,CHF,920,1200
spryker_drone_shipment-air_light,US,CHF,1400,1700
spryker_no_shipment,US,EUR,0,0
spryker_no_shipment,US,CHF,0,0
```

| COLUMN              | REQUIRED? | DATA TYPE | DATA EXAMPLE                    | DATA EXPLANATION                    |
|---------------------|-----------|-----------|---------------------------------|-------------------------------------|
| shipment_method_key | mandatory | string    | spryker_dummy_shipment-standard | Key of an existing shipping method. |
| store               | mandatory | string    | DE                              | Name of an existing store.          |
| currency            | mandatory | string    | EUR                             | Name of an existing currency.       |
| value_net           | optional  | integer   | 390                             | Net price in coins.                 |
| value_gross         | optional  | integer   | 490                             | Gross price in coins.               |

**vendor/spryker/spryker/Bundles/ShipmentTypeDataImport/data/import/shipment_type.csv**
```yaml
key,name,is_active
pickup,Pickup,1
delivery,Delivery,1
```

| COLUMN    | REQUIRED? | DATA TYPE | DATA EXAMPLE | DATA EXPLANATION             |
|-----------|-----------|-----------|--------------|------------------------------|
| key       | mandatory | string    | pickup       | Key for the shipment type.   |
| name      | mandatory | string    | Pickup       | Name for the shipment type.  |
| is_active | mandatory | string    | 1            | Status of the shipment type. |

**vendor/spryker/spryker/Bundles/ShipmentTypeDataImport/data/import/shipment_type_store.csv**
```yaml
shipment_type_key,store_name
pickup,AT
delivery,AT
pickup,DE
delivery,DE
pickup,US
delivery,US
```

| COLUMN            | REQUIRED? | DATA TYPE | DATA EXAMPLE | DATA EXPLANATION                  |
|-------------------|-----------|-----------|--------------|-----------------------------------|
| shipment_type_key | mandatory | string    | pickup       | Key of an existing shipping type. |
| store_name        | mandatory | string    | DE           | Name of an existing store.        |

**vendor/spryker/spryker/Bundles/ShipmentTypeDataImport/data/import/shipment_method_shipment_type.csv**
```yaml
shipment_method_key,shipment_type_key
spryker_dummy_shipment-standard,delivery
spryker_dummy_shipment-express,delivery
spryker_drone_shipment-air_standard,delivery
spryker_drone_shipment-air_sonic,delivery
spryker_drone_shipment-air_light,delivery
spryker_no_shipment,delivery
free_pickup,pickup
```

| COLUMN              | REQUIRED? | DATA TYPE | DATA EXAMPLE                    | DATA EXPLANATION                    |
|---------------------|-----------|-----------|---------------------------------|-------------------------------------|
| shipment_method_key | mandatory | string    | spryker_dummy_shipment-standard | Key of an existing shipping method. |
| shipment_type_key   | mandatory | string    | delivery                        | Key of an existing shipping type.   |

2. Register the following data import plugins:

| PLUGIN                                     | SPECIFICATION                                                             | PREREQUISITES | NAMESPACE                                                           |
|--------------------------------------------|---------------------------------------------------------------------------|---------------|---------------------------------------------------------------------|
| ShipmentDataImportPlugin                   | Imports shipment method data into the database.                           | None          | \Spryker\Zed\ShipmentDataImport\Communication\Plugin                |
| ShipmentMethodPriceDataImportPlugin        | Imports shipment method price data into the database.                     | None          | \Spryker\Zed\ShipmentDataImport\Communication\Plugin                |
| ShipmentMethodStoreDataImportPlugin        | Imports shipment method store data into the database.                     | None          | \Spryker\Zed\ShipmentDataImport\Communication\Plugin                |
| ShipmentTypeDataImportPlugin               | Imports shipment types data from the specified file.                      | None          | \Spryker\Zed\ShipmentTypeDataImport\Communication\Plugin\DataImport |
| ShipmentTypeStoreDataImportPlugin          | Imports shipment type stores data from the specified file.                | None          | \Spryker\Zed\ShipmentTypeDataImport\Communication\Plugin\DataImport |
| ShipmentMethodShipmentTypeDataImportPlugin | Imports shipment types for shipment methods data from the specified file. | None          | \Spryker\Zed\ShipmentTypeDataImport\Communication\Plugin\DataImport |

**src/Pyz/Zed/DataImport/DataImportDependencyProvider.php**

```php
<?php

namespace Pyz\Zed\DataImport;

use Spryker\Zed\DataImport\DataImportDependencyProvider as SprykerDataImportDependencyProvider;
use Spryker\Zed\ShipmentDataImport\Communication\Plugin\ShipmentDataImportPlugin;
use Spryker\Zed\ShipmentDataImport\Communication\Plugin\ShipmentMethodPriceDataImportPlugin;
use Spryker\Zed\ShipmentDataImport\Communication\Plugin\ShipmentMethodStoreDataImportPlugin;
use Spryker\Zed\ShipmentTypeDataImport\Communication\Plugin\DataImport\ShipmentMethodShipmentTypeDataImportPlugin;
use Spryker\Zed\ShipmentTypeDataImport\Communication\Plugin\DataImport\ShipmentTypeDataImportPlugin;
use Spryker\Zed\ShipmentTypeDataImport\Communication\Plugin\DataImport\ShipmentTypeStoreDataImportPlugin;

class DataImportDependencyProvider extends SprykerDataImportDependencyProvider
{
    /**
     * @return array
     */
    protected function getDataImporterPlugins(): array
    {
        return [
            new ShipmentDataImportPlugin(),
            new ShipmentMethodPriceDataImportPlugin(),
            new ShipmentMethodStoreDataImportPlugin(),
            new ShipmentTypeDataImportPlugin(),
            new ShipmentTypeStoreDataImportPlugin(),
            new ShipmentMethodShipmentTypeDataImportPlugin(),

        ];
    }
}
```

3. Enable the behaviors by registering the console commands:

**src/Pyz/Zed/Console/ConsoleDependencyProvider.php**

```php
<?php

namespace Pyz\Zed\Console;

use Spryker\Zed\Kernel\Container;
use Spryker\Zed\Console\ConsoleDependencyProvider as SprykerConsoleDependencyProvider;
use Spryker\Zed\DataImport\Communication\Console\DataImportConsole;
use Spryker\Zed\ShipmentDataImport\ShipmentDataImportConfig;
use Spryker\Zed\ShipmentTypeDataImport\ShipmentTypeDataImportConfig;

class ConsoleDependencyProvider extends SprykerConsoleDependencyProvider
{
    /**
     * @param \Spryker\Zed\Kernel\Container $container
     *
     * @return \Symfony\Component\Console\Command\Command[]
     */
    protected function getConsoleCommands(Container $container)
    {
        $commands = [
            new DataImportConsole(DataImportConsole::DEFAULT_NAME . ':' . ShipmentDataImportConfig::IMPORT_TYPE_SHIPMENT),
            new DataImportConsole(DataImportConsole::DEFAULT_NAME . ':' . ShipmentDataImportConfig::IMPORT_TYPE_SHIPMENT_PRICE),
            new DataImportConsole(DataImportConsole::DEFAULT_NAME . ':' . ShipmentDataImportConfig::IMPORT_TYPE_SHIPMENT_METHOD_STORE),
            new DataImportConsole(DataImportConsole::DEFAULT_NAME . ':' . ShipmentTypeDataImportConfig::IMPORT_TYPE_SHIPMENT_TYPE),
            new DataImportConsole(DataImportConsole::DEFAULT_NAME . ':' . ShipmentTypeDataImportConfig::IMPORT_TYPE_SHIPMENT_TYPE_STORE),
            new DataImportConsole(DataImportConsole::DEFAULT_NAME . ':' . ShipmentTypeDataImportConfig::IMPORT_TYPE_SHIPMENT_METHOD_SHIPMENT_TYPE),
        ];

        return $commands;
    }
}
```

4. Import data:

```bash
console data:import:shipment
console data:import:shipment-price
console data:import:shipment-method-store
console data:import shipment-type
console data:import shipment-type-store
console data:import shipment-method-shipment-type
```

{% info_block warningBox "Verification" %}

Make sure that the configured data has been added to the `spy_shipment_method`, `spy_shipment_method_price`, 
`spy_shipment_method_store`, `spy_shipment_type` and `spy_shipment_type_store` tables in the database.

{% endinfo_block %}

### 4) Set up behavior

1. Configure the data import to use your data on the project level:

**src/Pyz/Zed/ShipmentDataImport/ShipmentDataImportConfig**

```php
<?php

namespace Pyz\Zed\ShipmentDataImport;

use Generated\Shared\Transfer\DataImporterConfigurationTransfer;
use Spryker\Zed\ShipmentDataImport\ShipmentDataImportConfig as SprykerShipmentDataImportConfig;

class ShipmentDataImportConfig extends SprykerShipmentDataImportConfig
{
    /**
     * @return \Generated\Shared\Transfer\DataImporterConfigurationTransfer
     */
    public function getShipmentDataImporterConfiguration(): DataImporterConfigurationTransfer
    {
        return $this->buildImporterConfiguration('shipment.csv', static::IMPORT_TYPE_SHIPMENT);
    }

    /**
     * @return \Generated\Shared\Transfer\DataImporterConfigurationTransfer
     */
    public function getShipmentMethodPriceDataImporterConfiguration(): DataImporterConfigurationTransfer
    {
        return $this->buildImporterConfiguration('shipment_price.csv', static::IMPORT_TYPE_SHIPMENT_PRICE);
    }
}
```

**src/Pyz/Zed/ShipmentTypeDataImport/ShipmentTypeDataImportConfig**
```php
<?php

namespace Pyz\Zed\ShipmentTypeDataImport;

use Generated\Shared\Transfer\DataImporterConfigurationTransfer;
use Spryker\Zed\ShipmentTypeDataImport\ShipmentTypeDataImportConfig as SprykerShipmentTypeDataImportConfig;

class ShipmentTypeDataImportConfig extends SprykerShipmentTypeDataImportConfig
{
    /**
     * @return \Generated\Shared\Transfer\DataImporterConfigurationTransfer
     */
    public function getShipmentTypeDataImporterConfiguration(): DataImporterConfigurationTransfer
    {
        return $this->buildImporterConfiguration('shipment_type.csv', static::IMPORT_TYPE_SHIPMENT_TYPE);
    }

    /**
     * @return \Generated\Shared\Transfer\DataImporterConfigurationTransfer
     */
    public function getShipmentTypeStoreDataImporterConfiguration(): DataImporterConfigurationTransfer
    {
        return $this->buildImporterConfiguration('shipment_type_store.csv', static::IMPORT_TYPE_SHIPMENT_TYPE_STORE);
    }
    
    /**
     * @return \Generated\Shared\Transfer\DataImporterConfigurationTransfer
     */
    public function getShipmentMethodShipmentTypeDataImporterConfiguration(): DataImporterConfigurationTransfer
    {
        return $this->buildImporterConfiguration('shipment_method_shipment_type.csv', static::IMPORT_TYPE_SHIPMENT_METHOD_SHIPMENT_TYPE);
    }
}
```

2. Configure shipment GUI module with money and store plugins:

| PLUGIN                            | SPECIFICATION                                                                                              | PREREQUISITES | NAMESPACE                                             |
|-----------------------------------|------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------|
| MoneyCollectionFormTypePlugin     | Represents the money collection fields based on stores, currencies, and price types defined in the system. | None          | Spryker\Zed\MoneyGui\Communication\Plugin\Form        |
| StoreRelationToggleFormTypePlugin | Represents a store relation toggle form based on stores registered in the system.                          | None          | Spryker\Zed\Store\Communication\Plugin\Form           |
| ShipmentTotalCalculatorPlugin     | Calculates shipment total using expenses.                                                                  | None          | Spryker\Zed\Shipment\Communication\Plugin\Calculation |

**src/Pyz/Zed/ShipmentGui/ShipmentGuiDependencyProvider.php**

```php
<?php

namespace Pyz\Zed\ShipmentGui;

use Spryker\Zed\Kernel\Communication\Form\FormTypeInterface;
use Spryker\Zed\Kernel\Container;
use Spryker\Zed\MoneyGui\Communication\Plugin\Form\MoneyCollectionFormTypePlugin;
use Spryker\Zed\ShipmentGui\ShipmentGuiDependencyProvider as SprykerShipmentGuiDependencyProvider;
use Spryker\Zed\Store\Communication\Plugin\Form\StoreRelationToggleFormTypePlugin;

class ShipmentGuiDependencyProvider extends SprykerShipmentGuiDependencyProvider
{
    /**
     * @param \Spryker\Zed\Kernel\Container $container
     *
     * @return \Spryker\Zed\Kernel\Communication\Form\FormTypeInterface
     */
    protected function getMoneyCollectionFormTypePlugin(Container $container): FormTypeInterface
    {
        return new MoneyCollectionFormTypePlugin();
    }

    /**
     * @return \Spryker\Zed\Kernel\Communication\Form\FormTypeInterface
     */
    protected function getStoreRelationFormTypePlugin(): FormTypeInterface
    {
        return new StoreRelationToggleFormTypePlugin();
    }
}
```

{% info_block warningBox "Verification" %}

Make sure you can complete the following actions in the Back Office:

1. Navigate to **Administration&nbsp;<span aria-label="and then">></span> Shipments&nbsp;<span aria-label="and then">></span> Delivery Methods**. The **Delivery Methods** page opens.
2. Check that, in the **DELIVERY METHODS** table, the list of shipment methods is displayed.
3. Check that, for any shipment method of your choice, in the **Actions** column, you can click **View**, **Edit**, and **Delete** to complete a respective action.

{% endinfo_block %}

**src/Pyz/Zed/Calculation/CalculationDependencyProvider.php**

```php
<?php

namespace Pyz\Zed\Calculation;

use Spryker\Zed\Calculation\CalculationDependencyProvider as SprykerCalculationDependencyProvider;
use Spryker\Zed\Kernel\Container;
use Spryker\Zed\Shipment\Communication\Plugin\Calculation\ShipmentTotalCalculatorPlugin;

class CalculationDependencyProvider extends SprykerCalculationDependencyProvider
{
    protected function getQuoteCalculatorPluginStack(Container $container)
    {
        return [
            new ShipmentTotalCalculatorPlugin(),
        ];
    }
}
```

4. Configure the sales order item shipment expander plugins:

| PLUGIN                          | SPECIFICATION                                | PREREQUISITES | NAMESPACE                                                                       |
|---------------------------------|----------------------------------------------|---------------|---------------------------------------------------------------------------------|
| ShipmentOrderItemExpanderPlugin | Expands the sales order items with shipment. |               | Spryker\Zed\Shipment\Communication\Plugin\Sales\ShipmentOrderItemExpanderPlugin |


**src/Pyz/Zed/Sales/SalesDependencyProvider.php**

```php
<?php

namespace Pyz\Zed\Sales;

use Spryker\Zed\Sales\SalesDependencyProvider as SprykerSalesDependencyProvider;
use Spryker\Zed\Shipment\Communication\Plugin\Sales\ShipmentOrderItemExpanderPlugin;

class SalesDependencyProvider extends SprykerSalesDependencyProvider
{

 /**
     * @return array<\Spryker\Zed\SalesExtension\Dependency\Plugin\OrderItemExpanderPluginInterface>
     */
    protected function getOrderItemExpanderPlugins(): array
    {
        return [
            new ShipmentOrderItemExpanderPlugin(),
        ];
    }
}
```
