---
title: "HowTo: Create discounts based on shipment"
description: Use the guide to activate a discount rule based on a shipment carrier and add a shipment pre-check plugin to checkout.
last_updated: Jun 16, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/ht-activate-a-discount-rule-based-on-a-shipment-carrier
originalArticleId: 98408c10-05d0-4d84-a0a8-e01ba2cbdfea
redirect_from:
  - /2021080/docs/ht-activate-a-discount-rule-based-on-a-shipment-carrier
  - /2021080/docs/en/ht-activate-a-discount-rule-based-on-a-shipment-carrier
  - /docs/ht-activate-a-discount-rule-based-on-a-shipment-carrier
  - /docs/en/ht-activate-a-discount-rule-based-on-a-shipment-carrier
  - /v6/docs/ht-activate-a-discount-rule-based-on-a-shipment-carrier
  - /v6/docs/en/ht-activate-a-discount-rule-based-on-a-shipment-carrier
  - /v5/docs/ht-activate-a-discount-rule-based-on-a-shipment-carrier
  - /v5/docs/en/ht-activate-a-discount-rule-based-on-a-shipment-carrier
  - /v4/docs/ht-activate-a-discount-rule-based-on-a-shipment-carrier
  - /v4/docs/en/ht-activate-a-discount-rule-based-on-a-shipment-carrier
related:
  - title: Shipment feature overview
    link: docs/scos/user/features/shipment-feature-overview.html
  - title: "Reference information: Shipment method plugins"
    link: docs/scos/dev/feature-walkthroughs/shipment-feature-walkthrough/reference-information-shipment-method-plugins.html
---

The HowTo guide shows how to do the following:

* Activate a discount rule based on a shipment carrier, a shipment method or a shipment price.
* Add a shipment pre-check plugin to checkout.

## Activate a discount rule based on a shipment carrier

It is possible to create a discount rule based on a shipment carrier, a shipment method or a shipment price.

To have a discount calculated based on a shipment method, select the `shipment-method` rule in the discount UI, **Discount calculation**. Then, the discount applies only to the shipment expense with the chosen method. You could also select shipment-method rule for *Conditions* to define that your discount is applied only when the order is delivered by the chosen method.

The same approach works for a carrier (`shipment-carrier`) and price (`shipment.price`). You could combine these rules together based on your requirements.

To activate this feature, follow these steps:

1. In your project, install the `ShipmentDiscountConnector` module.
2. Activate the decision rule and the collector plugins in `\Pyz\Zed\Discount\DiscountDependencyProvider`:

```php
<?php

namespace Pyz\Zed\Discount;

use Spryker\Zed\ShipmentDiscountConnector\Communication\Plugin\DecisionRule\ShipmentCarrierDecisionRulePlugin;
use Spryker\Zed\ShipmentDiscountConnector\Communication\Plugin\DecisionRule\ShipmentMethodDecisionRulePlugin;
use Spryker\Zed\ShipmentDiscountConnector\Communication\Plugin\DecisionRule\ShipmentPriceDecisionRulePlugin;
use Spryker\Zed\ShipmentDiscountConnector\Communication\Plugin\DiscountCollector\ItemByShipmentCarrierPlugin;
use Spryker\Zed\ShipmentDiscountConnector\Communication\Plugin\DiscountCollector\ItemByShipmentMethodPlugin;
use Spryker\Zed\ShipmentDiscountConnector\Communication\Plugin\DiscountCollector\ItemByShipmentPricePlugin;
...

class DiscountDependencyProvider extends SprykerDiscountDependencyProvider
{

    /**
     * @return \Spryker\Zed\Discount\Dependency\Plugin\DecisionRulePluginInterface[]
     */
    protected function getDecisionRulePlugins()
    {
        return array_merge(parent::getDecisionRulePlugins(), [
            ...
            new ShipmentCarrierDecisionRulePlugin(),
            new ShipmentMethodDecisionRulePlugin(),
            new ShipmentPriceDecisionRulePlugin(),
        ]);
    }

    /**
     * @return \Spryker\Zed\Discount\Dependency\Plugin\CollectorPluginInterface[]
     */
    protected function getCollectorPlugins()
    {
        return array_merge(parent::getCollectorPlugins(), [
            ...
            new ItemByShipmentCarrierPlugin(),
            new ItemByShipmentMethodPlugin(),
            new ItemByShipmentPricePlugin(),
        ]);
    }

}
```

You are ready to use the shipment discounts.

## Checkout shipment pre-check plugin

You can add shipment pre-check plugin to checkout workflow, which checks if the shipment is active in order placing. If it's not, then error message is displayed and a customer gets redirected to the shipment step to select another shipment method.

1. Composer install a new module composer require `spryker/shipment-checkout-connector`. This module provides the plugin itself.
2. Add the `\Spryker\Zed\ShipmentCheckoutConnector\Communication\Plugin\Checkout\ShipmentCheckoutPreCheckPlugin` plugin to the checkout dependency provider pre-check plugin stack.

```php
<?php

namespace Pyz\Zed\Checkout;

	use Spryker\Zed\ShipmentCheckoutConnector\Communication\Plugin\Checkout\ShipmentCheckoutPreCheckPlugin;

	class CheckoutDependencyProvider extends SprykerCheckoutDependencyProvider
	{
	    /**
	       * @param \Spryker\Zed\Kernel\Container $container ’
	       *
	       * @return \Spryker\Zed\Checkout\Dependency\Plugin\CheckoutPreConditionInterface[]
	       */
	      protected function getCheckoutPreConditions(Container $container)
	      {
	          return [
	              ...//other plugins
	              new ShipmentCheckoutPreCheckPlugin()
	          ];
	      }
	}
```
