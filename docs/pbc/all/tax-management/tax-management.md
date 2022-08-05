---
title: Tax Management
description: With the Tax Management capability you can define taxes for the items you sell.
last_updated: Jun 25, 2021
template: concept-topic-template
originalLink: https://documentation.spryker.com/2021080/docs/tax-feature-overview
originalArticleId: 2ca980d2-d08b-4511-b26c-4cafa8624283
redirect_from:
  - /2021080/docs/tax-feature-overview
  - /2021080/docs/en/tax-feature-overview
  - /docs/tax-feature-overview
  - /docs/en/tax-feature-overview
  - /2021080/docs/tax
  - /2021080/docs/en/tax
  - /docs/tax
  - /docs/en/tax
  - /2021080/docs/international-tax-rates-sets-1
  - /2021080/docs/en/international-tax-rates-sets-1
  - /docs/international-tax-rates-sets-1
  - /docs/en/international-tax-rates-sets-1
  - /docs/scos/user/features/202200.0/tax-feature-overview.html
  - /docs/scos/user/features/202204.0/tax-feature-overview.html  
---

The *Tax Management* capability lets you define taxes for the items you sell. The capability is represented by two entities: tax rates and tax sets.

The tax rate is the percentage of the sales price that buyer pays as a tax. In the default Spryker implementation, the tax rate is defined per country where the tax applies. For details about how to create tax rates for countries in the Back Office, see [Create tax rates](/docs/pbc/all/tax-management/manage-in-the-back-office/create-tax-rates.html).

A tax set is a set of tax rates. You can [define tax sets in the Back office](/docs/pbc/all/tax-management/manage-in-the-back-office/create-tax-sets.html) or[ import tax sets](/docs/pbc/all/tax-management/import-and-export-data/import-tax-sets.html) into your project.

Tax sets can be applied to an abstract product, product option, and shipment:


| ENTITY | INSTRUCTIONS ON DEFINING TAX SETS FOR THE ENTITY IN THE BACK OFFICE  | DETAILS ON THE IMPORT FILE TO IMPORT TAX SETS FOR THE ENTITY |
| --- | --- | --- |
| Abstract product | [Define prices](/docs/scos/user/back-office-user-guides/{{site.version}}/catalog/products/manage-abstract-products-and-product-bundles/create-abstract-products-and-product-bundles.html#define-prices) | [File details: product_abstract.csv](/docs/scos/dev/data-import/{{site.version}}/data-import-categories/catalog-setup/products/file-details-product-abstract.csv.html) |
| Product option | [Creating a product option](/docs/scos/user/back-office-user-guides/{{site.version}}/catalog/product-options/create-product-options.html) | [File details: product_option.csv](/docs/scos/dev/data-import/{{site.version}}/data-import-categories/special-product-types/product-options/file-details-product-option.csv.html) |
| Shipment | [Add delivery methods](/docs/scos/user/back-office-user-guides/{{site.version}}/administration/delivery-methods/add-delivery-methods.html) | [File details: shipment.csv](/docs/scos/dev/data-import/{{site.version}}/data-import-categories/commerce-setup/file-details-shipment.csv.html) |

## International tax rates and sets

Align your business with international tax standards by defining tax rates and sets. Determine country-based tax rates for products, options, and shipments, that will automatically be applied to the respective shops.

In a tax system, the tax rate is the ratio (usually expressed as a percentage) at which a business, person, item is taxed.

A *tax set* is a set of tax rates that can be applied to a specific product.

Keeping that in mind, the tax rate is created first.
![Tax rate](https://spryker.s3.eu-central-1.amazonaws.com/docs/Features/Tax/International+Tax+Rates+&+Sets/tax-rate.gif)

Once the rate is defined, you can attach it to a tax set(s). A tax set can contain from one to many tax rates.
![Tax set](https://spryker.s3.eu-central-1.amazonaws.com/docs/Features/Tax/International+Tax+Rates+&+Sets/tax-set.gif)

The described values are defined in the **Back Office&nbsp;<span aria-label="and then">></span> Taxes** section.

![Tax section](https://spryker.s3.eu-central-1.amazonaws.com/docs/Features/Tax/International+Tax+Rates+&+Sets/taxes-section.gif)

## Avalara system for automated tax compliance

You can integrate the third-party system Avalara to automatically apply tax rates that depend on such factors as location, product type, and shipping rules.

{% info_block warningBox %}

Avalara is mostly meant for the USA.

{% endinfo_block %}

To use Avalara, [set up the AvaTax platform](https://help.avalara.com/Avalara_AvaTax_Update/Set_up_AvaTax_Update) for your application and [integrate Avalara](/docs/scos/dev/technology-partner-guides/{{site.version}}/taxes/avalara/integrating-avalara.html) into your project. Once you do that, you can [apply Avalara tax codes](https://help.avalara.com/Avalara_AvaTax_Update/Avalara_tax_codes) to automate tax calculations for your shop.

You can set the Avalara tax codes for the following entities by importing the codes:

* Abstract product: For details about import, see [File details: product_abstract.csv](/docs/scos/dev/data-import/{{site.version}}/data-import-categories/catalog-setup/products/file-details-product-abstract.csv.html).
* Product option: For details about import, see [File details: product_option.csv](/docs/scos/dev/data-import/{{site.version}}/data-import-categories/special-product-types/product-options/file-details-product-option.csv.html).
* Shipment: For details about import, see [File details: shipment.csv](/docs/scos/dev/data-import/{{site.version}}/data-import-categories/commerce-setup/file-details-shipment.csv.html).

{% info_block infoBox %}

Since shipment and products fall under different taxability categories, Avalara tax code for shipment is different from that of the abstract product or product option. For details about the codes and categories, see [Avalara tax code search](https://taxcode.avatax.avalara.com/).

{% endinfo_block %}

The Avalara codes are not displayed on the Storefront or in the Back Office. They are processed in the background to define taxes for order items. Avalara calculates taxes during the checkout, and, by default, the taxes are shown at the final checkout step.

When calculating taxes, Avalara takes the items' [warehouse addresses](/docs/scos/user/features/{{site.version}}/inventory-management-feature-overview.html#defining-a-warehouse-address) into account. Therefore, each order item you calculate a tax for with Avalara, must have a warehouse assigned. To learn how warehouses are assigned to order items by default, see [Warehouse assignment to order items (with Avalara integration only)](/docs/scos/user/features/{{site.version}}/inventory-management-feature-overview.html#warehouse-assignment-to-order-items-with-avalara-integration-only).

## Tax Management capability on the Storefront

A *product tax set* is calculated when buyers add products to the cart. Therefore, by default, the tax calculated on the basis of the product tax sets is displayed in the **Tax** section on the **Cart** page. However, the tax value on the **Cart** page is not always final because it does not take a possible shipment tax set into account since buyers select the shipping method during the checkout. If you have Avalara integrated, it calculates tax during the checkout as well. Therefore, the final tax value is always displayed only upon checkout.

Tax on the **Cart** page:

![image](https://spryker.s3.eu-central-1.amazonaws.com/docs/Features/Tax/tax-in-cart.png)

Tax in the checkout:

![image](https://spryker.s3.eu-central-1.amazonaws.com/docs/Features/Tax/tax-in-checkout.png)

## Current constraints

The capability has the following functional constraints:

* There is no Back Office UI for the Avalara tax codes.
* Many Avalara features are not supported yet. This will be resolved in the future.


## Related Business User articles

|BACK OFFICE USER GUIDES|
|---|
| [Create tax rates](/docs/pbc/all/tax-management/manage-in-the-back-office/create-tax-rates.html) |
| [Edit tax rates](/docs/pbc/all/tax-management/manage-in-the-back-office/edit-tax-rates.html) |
| [Create tax sets](/docs/pbc/all/tax-management/manage-in-the-back-office/create-tax-sets.html) |
| [Edit tax sets](/docs/pbc/all/tax-management/manage-in-the-back-office/edit-tax-sets.html) |

## Related Developer articles

| INTEGRATION GUIDES | MIGRATION GUIDES | GLUE API GUIDES | DATA IMPORT |
|---|---|---|---|
| [Avalara Tax integration](/docs/pbc/all/tax-management/third-party-integrations/integrate-avalara.html) | [Upgrade the Tax module](/docs/pbc/all/tax-management/install-and-upgrade/upgrade-the-tax-module.html) | [Retrieve tax sets](/docs/pbc/all/tax-management/manage-via-glue-api/retrieve-tax-sets.html) | [File details: tax.csv](/docs/pbc/all/tax-management/import-and-export-data/import-tax-sets.html) | |
| [Avalara Tax + Shipment feature integration](/docs/scos/dev/technology-partner-guides/{{site.version}}/taxes/avalara/integrating-avalara-tax-shipment.html) |  |  | [File details: product_abstract.csv](/docs/scos/dev/data-import/{{site.version}}/data-import-categories/catalog-setup/products/file-details-product-abstract.csv.html) | |
| [Avalara Tax + Product Options feature integration](/docs/pbc/all/tax-management/third-party-integrations/integrate-avalara-tax-product-options.html) |  |  | [File details: product_option.csv](/docs/scos/dev/data-import/{{site.version}}/data-import-categories/special-product-types/product-options/file-details-product-option.csv.html) | |
|  |  |  | [File details: shipment.csv](/docs/scos/dev/data-import/{{site.version}}/data-import-categories/commerce-setup/file-details-shipment.csv.html) |
