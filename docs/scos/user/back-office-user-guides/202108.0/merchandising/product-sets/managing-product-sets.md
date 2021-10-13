---
title: Managing product sets
description: Use these procedures to view, update or change the order of product sets, as well as activate/deactivate and/or delete them in the Back Office.
template: back-office-user-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/managing-product-sets
originalArticleId: eaa91090-6e3e-4af1-bc98-f9bae069939a
redirect_from:
  - /2021080/docs/managing-product-sets
  - /2021080/docs/en/managing-product-sets
  - /docs/managing-product-sets
  - /docs/en/managing-product-sets
---

This article describes how to manage product sets.

## Prerequisites

To start working with product sets, go to **Merchandising** > **Product Sets**.

For reference information, see [Reference information: Creating product sets](/docs/scos/user/back-office-user-guides/{{page.version}}/merchandising/product-sets/creating-product-sets.html#reference-information-creating-product-sets).

## Editing product sets

To edit a product set:
1. In the _Actions_ column of the *Product Sets* table, click **Edit** for the product set you want to update.
2. On the *Edit Product Set* page, update the needed attributes. The procedure is very similar to the procedure of creating a product set (see _Creating a Product Set_ article for more details). The only difference is that in the *Products* tab, in addition to the *Select Products to assign* table, you will see the *Products in this Set* table at the bottom of the page. In this table, you can:
    1. Clear the checkbox in the _Selected_ column to remove a specific product from the set.
    2. Define the position of the products in the set by putting the appropriate numbers in the _Position_ column. The product that has 0 in the _Position_ column goes first.
![Editing a product set](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Products/Products/Product+Sets/Managing+Product+Sets/editing-product-set.png)

{% info_block infoBox "Info" %}

The attributes you see are described in [Reference Information: Creating product sets](/docs/scos/user/back-office-user-guides/202108.0/merchandising/product-sets/creating-product-sets.html#reference-information-creating-product-sets).

{% endinfo_block %}

3. Click **Submit**.

**Tips & tricks**
On this page,  in the top right corner, you can click **View** and switch to the *View Product Set* page.

## Reordering product sets

The weight defines the order of the product sets displayed in the Product Sets section.

If you want to reorder the product sets, you:
1. In the top right corner of the *Product Sets* page, click **Reorder Product Sets**.
2. On the *Reorder Product Sets* page, define the order by putting the appropriate numbers in the _Weight_ column. Product sets with higher numbers are listed first.

![Reordering product sets](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Products/Products/Product+Sets/Managing+Product+Sets/reorder-product-sets.png)

3. Click **Submit**.

## Viewing product sets

To view a product set:
1. In the _Actions_ column of the *Product Sets* table, click **View** for the product set you want to view.
2. On this page, you can:
    1. Switch to the *Edit Product Set* page by clicking **Edit** in the top right corner.
    2. Deactivate a product set by clicking **Deactivate** in the top right corner.
    3. Open the *View Product Abstract* page of a specific product included in the set by clicking the hyperlinked product name in the _Product details_ column of the *Products* table.

## Activating and deactivating product sets

To activate/deactivate a product set:
1. In the _Actions_ column of the Product Sets table, click **Deactivate** for a specific product set.
    **Or**
2. Navigate to the **View Product Set** table, and in the top right corner, and click **Deactivate**.

## Deleting product set

To delete a product set, in the _Actions_ column of the *Product Sets* page, click **Delete**.

{% info_block infoBox "Info" %}

This will not delete the products included in this set. Those products will continue to exist in the system, and customers will be able to buy them. Only the logical connection between the products will be erased, and the product set will not be displayed for your customers.

{% endinfo_block %}
