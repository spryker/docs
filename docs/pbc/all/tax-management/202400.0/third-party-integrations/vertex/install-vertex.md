---
title: Install Vertex
description: Find out how you can install Vertex in your Spryker shop
draft: true
last_updated: Sep 13, 2023
template: howto-guide-template
related:
  - title: Vertex
    link: docs/pbc/all/tax-management/page.version/vertex/vertex.html
redirect_from:
    - /docs/pbc/all/tax-management/202307.0/vertex/install-vertex.html
    - /docs/pbc/all/tax-management/202400.0/base-shop/vertex/install-vertex.html

---

## Prerequisites

Before integrating Vertex, ensure the following prerequisites are met:

- Make sure your project is ACP-enabled. See [App Composition Platform installation](/docs/acp/user/app-composition-platform-installation.html) for details.

- The Vertex app catalog page lists specific packages that must be installed or upgraded before you can use the Vertex app. To check the list of the necessary packages, in the Back Office, go to **Apps**-> **Vertex**.
Ensure that your installation meets these requirements.

- Make sure that your deployment pipeline executes database migrations.

## 1. Integrate ACP connector module for tax calculation

To enable the Vertex integration, you need to integrate the [spryker/tax-app](https://github.com/spryker/tax-app) ACP connector module first.

To integrate the connector module for the Vertex app, follow the steps below.

### 1. Configure shared configs

Add the following config to `config/Shared/config_default.php`:

```php
// ...

use Generated\Shared\Transfer\ConfigureTaxAppTransfer;
use Generated\Shared\Transfer\DeleteTaxAppTransfer;
use Generated\Shared\Transfer\SubmitPaymentTaxInvoiceTransfer;
use Spryker\Shared\TaxApp\TaxAppConstants;
use Spryker\Zed\OauthAuth0\OauthAuth0Config;

// ...

$config[MessageBrokerConstants::MESSAGE_TO_CHANNEL_MAP] = [
    // ...
    ConfigureTaxAppTransfer::class => 'tax-commands',
    DeleteTaxAppTransfer::class => 'tax-commands',
    SubmitPaymentTaxInvoiceTransfer::class => 'payment-tax-invoice-commands',
];

$config[MessageBrokerAwsConstants::CHANNEL_TO_RECEIVER_TRANSPORT_MAP] = [
    // ...
    
    'tax-commands' => MessageBrokerAwsConfig::SQS_TRANSPORT,
];

$config[MessageBrokerAwsConstants::CHANNEL_TO_SENDER_TRANSPORT_MAP] = [
    // ...
    
    'payment-tax-invoice-commands' => 'http',
];

// ...

$config[TaxAppConstants::OAUTH_PROVIDER_NAME] = OauthAuth0Config::PROVIDER_NAME;
$config[TaxAppConstants::OAUTH_GRANT_TYPE] = OauthAuth0Config::GRANT_TYPE_CLIENT_CREDENTIALS;
$config[TaxAppConstants::OAUTH_OPTION_AUDIENCE] = 'aop-app';
```

### 2. Configure the Calculation dependency provider

Add the following to `src/Pyz/Zed/Calculation/CalculationDependencyProvider.php`:

```php
// ...

use Spryker\Zed\Calculation\Communication\Plugin\Calculator\GrandTotalCalculatorPlugin;
use Spryker\Zed\Calculation\Communication\Plugin\Calculator\TaxTotalCalculatorPlugin;
use Spryker\Zed\TaxApp\Communication\Plugin\Calculation\TaxAppCalculationPlugin;

// ...

    /**
     * @param \Spryker\Zed\Kernel\Container $container
     *
     * @return array<\Spryker\Zed\CalculationExtension\Dependency\Plugin\CalculationPluginInterface>
     */
    protected function getQuoteCalculatorPluginStack(Container $container): array
    {
        /** @var array<\Spryker\Zed\Calculation\Dependency\Plugin\CalculationPluginInterface> $pluginStack */
        $pluginStack = [
            // ...
        
            # This plugin should be put after other tax plugins, but before GrandTotalCalculatorPlugin.
            # Suggested plugins order is shown.
        
            new TaxTotalCalculatorPlugin(),
            new TaxAppCalculationPlugin(),
            new GrandTotalCalculatorPlugin(),
        
            // ...
        ];
        
        return $pluginStack;
    }
    
    /**
     * @param \Spryker\Zed\Kernel\Container $container
     *
     * @return array<\Spryker\Zed\CalculationExtension\Dependency\Plugin\CalculationPluginInterface>
     */
    protected function getOrderCalculatorPluginStack(Container $container): array
    {
        return [
            // ...
        
            # This plugin should be put after other tax plugins, but before GrandTotalCalculatorPlugin.
            # Suggested plugins order is shown.
        
            new TaxTotalCalculatorPlugin(),
            new TaxAppCalculationPlugin(),
            new GrandTotalCalculatorPlugin(),
        
            // ...
        ];
    }

// ...
```

{% info_block infoBox "Performance improvement" %}

Spryker has its own [Taxes](/docs/pbc/all/tax-management/{{page.version}}/spryker-tax\base-shop/tax-feature-overview.html) feature, which comes pre-installed in the Checkout through the Calculation module. To enhance performance when using an external Tax calculation provider, we recommend disabling the following plugins:

in `\Pyz\Zed\Calculation\CalculationDependencyProvider::getQuoteCalculatorPluginStack()`:

- TaxAmountCalculatorPlugin
- ItemTaxAmountFullAggregatorPlugin
- TaxRateAverageAggregatorPlugin
- TaxTotalCalculatorPlugin

in `\Pyz\Zed\Calculation\CalculationDependencyProvider::getOrderCalculatorPluginStack()`:

- TaxAmountCalculatorPlugin
- ItemTaxAmountFullAggregatorPlugin
- TaxAmountAfterCancellationCalculatorPlugin
- OrderTaxTotalCalculationPlugin

Disabling them will also disable Spryker Taxes feature. This means that in case when Vertex is unresponsive or disabled order taxes will not be calculated and their amount will be always 0.

{% endinfo_block %}

### 3. Configure the Shop Application dependency provider

Add the following code to `src/Pyz/Yves/ShopApplication/ShopApplicationDependencyProvider.php`:

```php

namespace Pyz\Yves\ShopApplication;

use SprykerShop\Yves\ShopApplication\ShopApplicationDependencyProvider as SprykerShopApplicationDependencyProvider;
use SprykerShop\Yves\CartPage\Widget\CartSummaryHideTaxAmountWidget;

class ShopApplicationDependencyProvider extends SprykerShopApplicationDependencyProvider
{
    /**
     * @phpstan-return array<class-string<\Spryker\Yves\Kernel\Widget\AbstractWidget>>
     *
     * @return array<string>
     */
    protected function getGlobalWidgets(): array
    {
        return [
            // ...

            # This widget is replacing Spryker OOTB tax display in cart summary page with text stating that tax amount will be calculated during checkout process.
            CartSummaryHideTaxAmountWidget::class,
        ];
    }
}

```


### 4. Configure the Message Broker dependency provider

Add the following code to `src/Pyz/Zed/MessageBroker/MessageBrokerDependencyProvider.php`:

```php

namespace Pyz\Zed\MessageBroker;

use Spryker\Zed\MessageBroker\MessageBrokerDependencyProvider as SprykerMessageBrokerDependencyProvider;
use Spryker\Zed\TaxApp\Communication\Plugin\MessageBroker\TaxAppMessageHandlerPlugin;

class MessageBrokerDependencyProvider extends SprykerMessageBrokerDependencyProvider
{
    /**
     * @return array<\Spryker\Zed\MessageBrokerExtension\Dependency\Plugin\MessageHandlerPluginInterface>
     */
    public function getMessageHandlerPlugins(): array
    {
        return [
            // ...

            # This plugin is handling messages sent from Vertex app to SCCOS.
            new TaxAppMessageHandlerPlugin(),
        ];
    }
}

```

### 5. (Optional) If you plan to send invoices to Vertex through OMS, configure your Payment OMS

Configure payment `config/Zed/oms/{your_payment_oms}.xml`as in the following example:

```xml
<?xml version="1.0"?>
<statemachine
    xmlns="spryker:oms-01"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="spryker:oms-01 http://static.spryker.com/oms-01.xsd"
>

    <process name="SomePaymentProcess" main="true">

        <!-- other configurations -->
        
        <states>

            <!-- other states -->
            
            <state name="tax invoice submitted" reserved="true" display="oms.state.paid"/>

            <!-- other states -->
            
        </states>

        <transitions>

            <!-- other transitions -->

            <transition happy="true">
                <source>paid</source> <!-- Suggested that paid transition should be the source, but it's up to you -->
                <target>tax invoice submitted</target>
                <event>submit tax invoice</event>
            </transition>

            <!-- other transitions -->

            <transition happy="true">
                <source>tax invoice submitted</source>
                
                <!-- Here are the contents of the target transition -->
                
            </transition>

            <!-- other transitions -->
            
        </transitions>

        <events>

            <!-- other events -->

            <event name="submit tax invoice" onEnter="true" command="TaxApp/SubmitPaymentTaxInvoice"/>

            <!-- other events -->
            
        </events>
        
    </process>
    
</statemachine>
```

#### Configure the Oms dependency provider
Add the config to `src/Pyz/Zed/Oms/OmsDependencyProvider.php`:

```php
// ...
    
use Spryker\Zed\TaxApp\Communication\Plugin\Oms\Command\SubmitPaymentTaxInvoicePlugin;

// ...

    /**
     * @param \Spryker\Zed\Kernel\Container $container
     *
     * @return \Spryker\Zed\Kernel\Container
     */
    protected function extendCommandPlugins(Container $container): Container
    {
         $container->extend(self::COMMAND_PLUGINS, function (CommandCollectionInterface $commandCollection) {
             
             // ...
             
             $commandCollection->add(new SubmitPaymentTaxInvoicePlugin(), 'TaxApp/SubmitPaymentTaxInvoice');

             // ...
            
             return $commandCollection;
        });
        
        return $container;
    }

```

## 2. Integrate the Vertex app

Spryker does not have the same data model as Vertex, which is necessary for accurate tax calculations. Therefore, the integration requires project developers to to add some missing information to the Quote object before sending a calculation request.

The following diagram shows the data flow of the tax calculation request from Spryker Cart to the Vertex API.

 ![tax-calculation-request](https://spryker.s3.eu-central-1.amazonaws.com/docs/pbc/all/tax-management/vertex/install-vertex/tax-calculation-requests.png)

### 1. Configure Vertex-specific metadata transfers

Define specific Vertex Tax metadata transfers and extend other transfers with them:

```xml

<?xml version="1.0"?>
<transfers xmlns="spryker:transfer-01"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="spryker:transfer-01
    http://static.spryker.com/transfer-01.xsd">

    <!-- Calculable Object is extended with SaleTaxMetadata -->
    <transfer name="CalculableObject">
        <property name="taxMetadata" type="SaleTaxMetadata" strict="true"/>
    </transfer>

    <!-- Order is extended with SaleTaxMetadata -->
    <transfer name="Order">
        <property name="taxMetadata" type="SaleTaxMetadata" strict="true"/>
    </transfer>

    <!-- Expense is extended with ItemTaxMetadata -->
    <transfer name="Expense">
        <property name="taxMetadata" type="ItemTaxMetadata" strict="true"/>
    </transfer>

    <!-- Item is extended with ItemTaxMetadata -->
    <transfer name="Item">
        <property name="taxMetadata" type="ItemTaxMetadata" strict="true"/>
    </transfer>

    <!-- Product Option is extended with ItemTaxMetadata -->
    <transfer name="ProductOption">
        <property name="taxMetadata" type="ItemTaxMetadata" strict="true"/>
    </transfer>

    <!-- Sales Tax Metadata. It contains Vertex tax metadata which is related to Order or Quote in general. -->
    <transfer name="SaleTaxMetadata" strict="true">
        <property name="seller" type="array" associative="true" singular="_"/>
        <property name="customer" type="array" associative="true" singular="_"/>
    </transfer>

    <!-- Items Tax Metadata. It contains Vertex tax metadata which is related to Item.-->
    <transfer name="ItemTaxMetadata" strict="true">
        <property name="product" type="array" associative="true" singular="_"/>
        <property name="flexibleFields" type="array" associative="true" singular="_"/>
    </transfer>

</transfers>

```

`SaleTaxMetadata` and `ItemTaxMetadata` are designed to be equal to the Vertex Tax Calculation API request body. You can extend them as you need, following to the Vertex API structure.

- `SaleTaxMetadata` equals the Invoicing/Quotation request payload, excluding LineItems.

- `ItemTaxMetadata` equals the Line Item API payload.

### 2. Implement Vertex-specific metadata extender plugins

There are several types of expander plugins you have to introduce.
As a starting point, you can take examples provided by Spryker in the [tax-app-vertex](https://github.com/spryker/tax-app-vertex) module. The plugins inside are for development purposes. The data in the TaxMetaData fields has to be collected from the project database or other sources such as external ERP.

#### Configure the Customer Class Code Expander plugins

The following code sample shows how to introduce the following expander plugin:

`Pyz/Zed/{YourDesiredModule}/Communication/Plugin/Order/OrderCustomerWithVertexCodeExpanderPlugin.php`

```php
<?php

namespace Pyz\Zed\{YourDesiredModule}\Communication\Plugin\Order;

use Generated\Shared\Transfer\OrderTransfer;
use Spryker\Zed\Kernel\Communication\AbstractPlugin;
use Spryker\Zed\TaxAppExtension\Dependency\Plugin\OrderTaxAppExpanderPluginInterface;

class OrderCustomerWithVertexCodeExpanderPlugin extends AbstractPlugin implements OrderTaxAppExpanderPluginInterface
{
    /**
     * @param \Generated\Shared\Transfer\OrderTransfer $orderTransfer
     *
     * @return \Generated\Shared\Transfer\OrderTransfer
     */
    public function expand(OrderTransfer $orderTransfer): OrderTransfer
    {
        $orderTransfer->getTaxMetadata()->setCustomer(['customerCode' => ['classCode' => 'vertex-customer-code']]);

        return $orderTransfer;
    }
}
```

The following code sample shows how to introduce the following expander plugin:

`Pyz/Zed/{YourDesiredModule}/Communication/Plugin/Quote/CalculableObjectCustomerWithVertexCodeExpanderPlugin.php`


```php
<?php

namespace Spryker\Zed\{YourDesiredModule}\Communication\Plugin\Quote;

use Generated\Shared\Transfer\CalculableObjectTransfer;
use Spryker\Zed\Kernel\Communication\AbstractPlugin;
use Spryker\Zed\TaxAppExtension\Dependency\Plugin\CalculableObjectTaxAppExpanderPluginInterface;

class CalculableObjectCustomerWithVertexCodeExpanderPlugin extends AbstractPlugin implements CalculableObjectTaxAppExpanderPluginInterface
{
    /**
     * @param \Generated\Shared\Transfer\CalculableObjectTransfer $calculableObjectTransfer
     *
     * @return \Generated\Shared\Transfer\CalculableObjectTransfer
     */
    public function expand(CalculableObjectTransfer $calculableObjectTransfer): CalculableObjectTransfer
    {
        $calculableObjectTransfer->getTaxMetadata()->setCustomer(['customerCode' => ['classCode' => 'vertex-customer-code']]);

        return $calculableObjectTransfer;
    }
}
```

#### Configure the Customer Exemption Certificate Expander plugins

Configure the Customer Exemption Certificate Expander plugin for order:

`Pyz/Zed/{YourDesiredModule}/Communication/Plugin/Order/OrderCustomerWithVertexExemptionCertificateExpanderPlugin.php`

Configure the Customer Exemption Certificate Expander plugin for quote:

`Pyz/Zed/{YourDesiredModule}/Communication/Plugin/Quote/CalculableObjectCustomerWithVertexExemptionCertificateExpanderPlugin.php`

The following code sample shows how to implement the previously mentioned plugins:

```php
// ...
class OrderCustomerWithVertexExemptionCertificateExpanderPlugin extends AbstractPlugin implements CalculableObjectTaxAppExpanderPluginInterface
{
    /**
     * @param \Generated\Shared\Transfer\CalculableObjectTransfer $calculableObjectTransfer
     *
     * @return \Generated\Shared\Transfer\CalculableObjectTransfer
     */
    public function expand(CalculableObjectTransfer $calculableObjectTransfer): CalculableObjectTransfer
    {
        $calculableObjectTransfer->getTaxMetadata()->setCustomer(['exemptionCertificate' => ['exemptionCertificateNumber' => 'vertex-exemption-certificate-number']]);

        return $calculableObjectTransfer;
    }
}
```

#### Configure the Product Class Code Expander plugins

Configure the Product Class Code Expander plugin for order items:

`Pyz/Zed/{YourDesiredModule}/Communication/Plugin/Order/OrderItemVertexProductClassCodeExpanderPlugin.php`

Configure the Product Class Code Expander plugin for quote items:

`Pyz/Zed/{YourDesiredModule}/Communication/Plugin/Quote/CalculableObjectItemWithVertexProductClassCodeExpanderPlugin.php`

The contents of both plugins are similar:

```php
// ...
class ItemWithVertexClassCodeExpanderPlugin extends AbstractPlugin implements CalculableObjectTaxAppExpanderPluginInterface
{
    /**
     * @param \Generated\Shared\Transfer\CalculableObjectTransfer $calculableObjectTransfer
     *
     * @return \Generated\Shared\Transfer\CalculableObjectTransfer
     */
    public function expand(CalculableObjectTransfer $calculableObjectTransfer): CalculableObjectTransfer
    {
        foreach ($calculableObjectTransfer->getItems() as $itemTransfer) {
            $itemTransfer->getTaxMetadata()->setProduct(['productClass' => 'vertex-product-class-code']);
        }

        return $calculableObjectTransfer;
    }
}
```

{% info_block infoBox "Use same Product Class Code" %}

You must use the same Product Class Code extension for all product options and other order expenses. From Vertex's perspective, it considers each of them as a separate item for tax calculation. For guidance on where to place them, refer to the definition of transfers in [Configure Vertex-specific Metadata Transfers](#1-configure-vertex-specific-metadata-transfers).

{% endinfo_block %}

#### Configure the flexible fields extension

Configure the flexible files extension as in the following example:

```php

class ItemWithFlexibleFieldsExpanderPlugin extends AbstractPlugin implements CalculableObjectTaxAppExpanderPluginInterface
{
    // ...
    
    /**
     * @param \CalculableObjectTransfer $calculableObjectTransfer
     * 
     * @return \CalculableObjectTransfer
     */
    public function expand(CalculableObjectTransfer $calculableObjectTransfer): CalculableObjectTransfer
    {
        foreach ($calculableObjectTransfer->getItems() as $itemTransfer) {
            $itemTransfer
                ->getTaxMetadata()
                ->setFlexibleFields(
                    [
                        'flexibleCodeFields' => [
                            [
                                'fieldId' => 1,
                                'value' => 'vertex-flexible-code-value',
                            ],
                        ],
                    ],
                );
        }

        return $calculableObjectTransfer;
    }
}
```

### 3. Configure the Tax App dependency provider

After the Tax App dependency provider configuration, the plugin stack will look similar to this one:

```php

namespace Pyz\Zed\TaxApp;

// The following plugins are for Marketplace only.
use Spryker\Zed\MerchantProfile\Communication\Plugin\TaxApp\MerchantProfileAddressCalculableObjectTaxAppExpanderPlugin;
use Spryker\Zed\MerchantProfile\Communication\Plugin\TaxApp\MerchantProfileAddressOrderTaxAppExpanderPlugin;
use Spryker\Zed\ProductOfferAvailability\Communication\Plugin\TaxApp\ProductOfferAvailabilityCalculableObjectTaxAppExpanderPlugin;
use Spryker\Zed\ProductOfferAvailability\Communication\Plugin\TaxApp\ProductOfferAvailabilityOrderTaxAppExpanderPlugin;

class TaxAppDependencyProvider extends SprykerTaxAppDependencyProvider
{
    /**
     * @return array<\Spryker\Zed\TaxAppExtension\Dependency\Plugin\CalculableObjectTaxAppExpanderPluginInterface>
     */
    protected function getCalculableObjectExpanderPluginCollection(): array
    {
        return [       
            # This plugin stack is responsible for expansion of CalculableObjectTransfer based on present fields. Add your custom implemented expander plugins here following the example in `spryker/tax-app-vertex` module.
            
            // The following plugins are for Marketplace only.
            # This plugin is expanding CalculableObjectTransfer object with merchant address information.
            new MerchantProfileAddressCalculableObjectTaxAppExpanderPlugin(),
            # This plugin is expanding CalculableObjectTransfer object with product offer availability information.
            new ProductOfferAvailabilityCalculableObjectTaxAppExpanderPlugin(),
        ];
    }

    /**
     * @return array<\Spryker\Zed\TaxAppExtension\Dependency\Plugin\OrderTaxAppExpanderPluginInterface>
     */
    protected function getOrderExpanderPluginCollection(): array
    {
        return [
            # This plugin stack is responsible for expansion of OrderTransfer based on present fields. Add your custom implemented expander plugins here following the example in `spryker/tax-app-vertex` module.
            
            // The following plugins are for Marketplace only.
            # This plugin is expanding OrderTransfer object with merchant address information.
            new MerchantProfileAddressOrderTaxAppExpanderPlugin(),
            # This plugin is expanding OrderTransfer object with product offer availability information.
            new ProductOfferAvailabilityOrderTaxAppExpanderPlugin(),
        ];
    }
}

```

### 4. Configure Product Offer Stock dependency provider (Marketplace only)

After you configured the Product Offer Stock dependency provider for Marketplace, the plugin stack will look similar to this one:

```php

namespace Pyz\Zed\ProductOfferStock;

use Spryker\Zed\ProductOfferStock\ProductOfferStockDependencyProvider as SprykerProductOfferStockDependencyProvider;
use Spryker\Zed\StockAddress\Communication\Plugin\Stock\StockAddressStockTransferProductOfferStockExpanderPlugin;

class ProductOfferStockDependencyProvider extends SprykerProductOfferStockDependencyProvider
{
    /**
     * @return array<\Spryker\Zed\ProductOfferStockExtension\Dependency\Plugin\StockTransferProductOfferStockExpanderPluginInterface>
     */
    protected function getStockTransferExpanderPluginCollection(): array
    {
        return [
            # This plugin is providing warehouse address to StockTransfer objects which is used during tax calculation.
            new StockAddressStockTransferProductOfferStockExpanderPlugin(),
        ];
    }
}

```
