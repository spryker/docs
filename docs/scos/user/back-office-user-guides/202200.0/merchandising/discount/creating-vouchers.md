---
title: Creating vouchers
description: Use the procedure to create discount vouchers your customer can redeem during checkout.
last_updated: Aug 27, 2021
template: back-office-user-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/creating-a-voucher
originalArticleId: 5d9e5e07-5260-4f0a-8118-aaa324af6fbc
redirect_from:
  - /2021080/docs/creating-a-voucher
  - /2021080/docs/en/creating-a-voucher
  - /docs/creating-a-voucher
  - /docs/en/creating-a-voucher
related:
  - title: Creating cart rules
    link: docs/scos/user/back-office-user-guides/page.version/merchandising/discount/creating-cart-rules.html
---

This guide describes how to create a voucher.

Vouchers are codes that customers can redeem during checkout. Voucher codes are grouped into pools to apply logic to multiple vouchers at once. You can generate a single voucher to be used by multiple customers or a pool of dedicated one-time per-customer voucher codes.

## Prerequisites

To start working with discounts, navigate to **Merchandising** > **Discount**.

Review the reference information before you start, or just look up the necessary information as you go through the process.

## Creating a voucher

To create a discount voucher:
1. On the **Discount** page,  in the top-right corner, click **Create new discount**.
2. On the **Create new discount** page, on the **General Information** tab, do the following:
    1. In **STORE RELATION**, select the stores where you want the discount to be active.
    2. In the **DISCOUNT TYPE** drop-down, select **Voucher codes**.
    3. In the **NAME** field, specify the name of the voucher.
    4. _Optional_: in the **DESCRIPTION** field, enter the description of the voucher.
    5. _Optional_: in the **PRIORITY** field, enter an integer value from `1` to `9999` for the discount voucher priority. For reference information, see [General Information tab](#general-information-tab).
    6. Specify if the voucher is exclusive. For reference information, see [General information tab](#general-information-tab).
    7. Specify the validity interval (lifetime) of the voucher.
3. To proceed, click **Next** or select the **Discount calculation** tab.
4. On the **Discount calculation** tab, do the following:
    1.  In the **CALCULATOR TYPE** drop-down, select either **Percentage** or **Fixed amount**. For reference information, see the [Discount calculation tab](#discount-calculation-tab).

      {% info_block warningBox "Note" %}

      The next step varies based on the selected calculator type:

      1. *Fixed amount*: Enter the amounts (per currency and price mode, if applicable) to be discounted.

      2. *Percentage*: Enter the percent value to be discounted.

      {% endinfo_block %}

    2. Select the **Discount application type** and define the products to which the voucher should be applied. See reference information of the [Discount calculation](#discount-calculation-tab) tab for more details.
5. Click **Next**, or select the **Conditions** tab to proceed.
6. On the **Conditions** tab, do the following:
    1. Select the **APPLY WHEN** conditions or click **Plain query** and enter the  query manually. See reference information of the [Conditions](#conditions) tab for more details.
    2. Enter the value for the **THE DISCOUNT CAN BE APPLIED IF THE QUERY APPLIES FOR AT LEAST X ITEM(S).** field.
7. To create the new voucher, click **Save**.

When you click **Save**, an additional tab named **Voucher Codes** appears. Here, you can generate, view, and export voucher codes (if they were already created).
The list is empty until codes are generated.

On the **Voucher code** tab, do the following:
1. Enter the **QUANTITY** for voucher codes you want to generate.
2. *Optional*: In **CUSTOM CODE**, enter any text that you would like to precede the randomly generated characters in each voucher code. You can also use the placeholder *[code]* to specify the location.
3. Set the **ADD RANDOM GENERATED CODE LENGTH** by selecting the value from a drop-down list.
4. Set **MAX NUMBER OF USES**.
5. To complete the process, click **Generate**.
    The voucher codes are generated according to your specifications. The codes are displayed in the table at the bottom of the page.
5. To activate the voucher, in the top right corner, click **Activate**.

Even if a voucher is valid and the decision rules are satisfied, a voucher can only be redeemed if it's currently active.

{% info_block infoBox %}

See [Voucher code](#voucher-code) for more information.

{% endinfo_block %}

**Tips & tricks**

Once you generated voucher codes, you can export them as a CSV file.
To do that, below *Generate*, click **Export** .

## Reference information: Creating a voucher

This section describes attributes you enter and select when creating or editing a voucher.

### <a name="discount-overview-page"></a>Discount Overview page

In the **Discount** section, you see the following:
* The discount ID and name.
* Type of the discount, its validity period, priority, and status.
* Identifier for exclusive discounts.
* Stores where the discount applies.
* Actions that you can do on each specific discount.

By default, the last created discount goes on top of the table. However, you can sort and search the list of discounts.

All columns with headers having arrows in the DISCOUNT LIST table are sortable.

**Actions column**

All the discount management options you can invoke from the *Actions* column are described in the following table.

| ACTION |DESCRIPTION  |
| --- | --- |
|Edit  | Takes you to the *Edit Discount* page. Here, you can modify discount settings or generate voucher codes if it is a voucher discount. |
|  View| Takes you to the *View Discount* page. Here, you can find all the information about the chosen discount. |
|  Add code| You can see this action only if the chosen discount is of a voucher type. It takes you directly to the *Voucher codes* tab of the *Edit Discount* page. Here, you can generate new voucher codes, export or delete the ones that are already created. |
| Activate/Deactivate | Activates or deactivates a specific discount. If a voucher discount is deactivated, its codes are invalid when entered in a cart. If a cart rule is deactivated, it won't be automatically applied even if the discount rules are fulfilled. |

### Create new discount page

This section describes attributes you select and enter on the *Create Discount* and *Edit Discount* pages when creating and editing a discount.

#### General information tab

The following table describes the attributes you enter and select in the *General information* tab:

| ATTRIBUTE |DESCRIPTION  |
| --- | --- |
|STORE RELATION  |Stores the discount is to be active in. You can select multiple stores.|
| DISCOUNT TYPE | Drop-down list where you select either *Voucher code* or *Cart rule* discount type. |
| NAME | A unique name that is displayed in the calculation section of the cart on the Storefront. Should be short, but descriptive. |
| DESCRIPTION | A summary explaining the promotion. Displayed with eligible products where applicable.|
| PRIORITY | Defines [the discount priority](/docs/scos/user/features/{{page.version}}/promotions-discounts-feature-overview.html#discount-priority). Represented as an integer value from 1 to 9999, 1 being the highest priority and 9999 the lowest. |
| NON-EXCLUSIVE | Defines the discount exclusivity. Buyers can redeem non-exclusive discounts in conjunction with other non-exclusive discounts.|
| EXCLUSIVE | Defines the discount exclusivity. When a discount is exclusive, no other discounts may be applied in conjunction. When a cart is eligible for multiple exclusive discounts, the discount with the highest value to the customer is applied. The exception to this is promotional product discounts. Query string discounts and promotional product discounts exclude only among each other. Promotional product discounts are not affected by exclusive query string discounts and conversely.|
| VALID FROM and VALID TO | Vouchers are redeemable or the cart rule is active between **VALID FROM** and **VALID TO** dates and times (in UTC), inclusive. For example, a voucher can be redeemed or discount applies to the cart starting from 01.12.2021 23:00 until 31.01.2022 22:59, UTC. |

{% info_block infoBox "Info" %}

It is important to name and describe the discount in a way that is meaningful for other Back Office users. Besides, the given name is displayed in the customer's cart when redeeming the voucher. Therefore, it must be unique.

{% endinfo_block %}

#### <a name="discount-calculation-tab"></a>Discount calculation tab

This section contains information you need to know when working with discount calculations in the *Discount calculation* tab.

**CALCULATOR TYPE**

The discount can be calculated in two ways:
* *Percentage*: The discount is calculated as a percentage of the discounted items' prices. If selected, you need to set the percentage value (for example, 25)
* *Fixed amount*: A fixed amount is discounted. If you select this type, you need to specify the amount (Gross, Net, or Both) for each currency used in your store.

Example:

| PRODUCT PRICE | CALCULATOR PLUGIN | AMOUNT | DISCOUNT APPLIED | PRICE TO PAY |
| --- | --- | --- | --- | --- |
| 50 € | Percentage | 10 |5 € | 45 € |
| 50 €| Fixed amount | 10 €| 10 €| 40 €|

**DISCOUNT APPLICATION TYPE**

You can select one of the following options:
* Query String
* Promotional Product

**Query String**

You can use a query to define discount conditions. Only products that satisfy the query's conditions are discountable. Queries also define if the discount is applied to one or several products. Discount conditions are set by using either the *query builder* or by specifying a *Plain query*.

Use the query builder to construct queries (guided) or the **Plain query** field to enter them (free text). You can switch between both modes by clicking the corresponding button (note that incomplete queries cannot be transferred between the two modes).

**Query builder**

![Discount_Calculation_Query](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Discount/Discount+Calculation:+Reference+Information/query-string.png)

**Plain Query**

![Discount_Calculation_Plain Query](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Discount/Discount+Calculation:+Reference+Information/discount-calculation-plain-query.png)

The query builder lets you combine different conditions with connectors (**AND** and **OR**). Multiple conditions (rules) can be added and grouped in this way. Each condition (rule) consists of:
* Field (for example, attribute.color)
* Operator (for example, equal(=))
* Value tokens (for example, blue)

{% info_block infoBox "Info" %}

The fields and values are defined by your shop data.

{% endinfo_block %}

These tokens are used to build plain queries too. The pattern of the plain query is as follows:
![Plain Query Pattern](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Discount/Discount+Calculation:+Reference+Information/plain-query-pattern.png)

You can find plain query examples in the following table.

|PLAIN QUERY|EXPLANATION|
|---|---|
|day-of-week = '1'|Discount applies if the order is placed on Monday.|
|shipment-carrier != '1' AND price-mode = 'GROSS_MODE'|Discount applies if the shipment carrier with the attribute "1" is not chosen and gross pricing is selected.|
|currency != 'EUR' OR price-mode = 'GROSS_MODE'|Discount applies if the selected currency is not Euro or the pricing mode is gross.|

{% info_block infoBox "Info" %}

See [Token description tables](#token-description-tables) for more information.

{% endinfo_block %}

**Promotional product discount**

This discount type lets you discount a specific product at a fixed quantity whenever the discount conditions are met. A common use case is for a "buy x, get y" discount where a customer gets an item for free when they buy a certain product or spend a certain amount. The product you are promoting goes in the **Abstract product SKU** field. The **Quantity** field represents the limit on the number of items eligible for the discount. When a customer fulfills the discount conditions, the promotional product is automatically merchandised below the items in a customer's cart. The customer can either add the product to the cart from this widget or any other place in the shop, and the discount will apply. It is important to note that the promotional product discount only applies if the product is added to the cart after meeting the discount's conditions. If the product is already in the cart before the discount conditions are met, the customer needs to remove and re-add it.
![Application type](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Discount/Discount+Calculation:+Reference+Information/Application+type.png)

You can either give away the promotional product completely for free or provide a discount for this product by specifying the percentage value or a fixed amount to be discounted from the promotional product's price (when giving the product for free, the percentage value should be 100%, while the fixed-price value should be equal to the product's price).

#### <a name="conditions"></a>Conditions

This section provides information that you need to know when working with discount conditions in the *Conditions* tab.

Conditions are also called decision rules.

* A cart rule can have one or more conditions linked to it. The cart rule is redeemed only if every condition linked to it is satisfied.
* Vouchers can be linked to one or more conditions. Vouchers are only redeemed if all linked conditions are satisfied.

The conditions are created in the form of a query and may be entered as a plain query or via the query builder. For more details, see the [Discount calculation tab](#discount-calculation-tab) section.

{% info_block infoBox "Info" %}

If you do not need to add a condition, you can leave the query builder empty.

{% endinfo_block %}

Example: Discount is applied if five or more items are in the cart and it is Tuesday or Wednesday.
![Discount Condition](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Discount/Discount+Conditions:+Reference+Information/discount-condition.png)

The minimum order amount value specifies the threshold which should be reached for the products in a cart with a certain attribute to be discounted. When added to cart, products with the attribute specified by a query are measured against the threshold. By default, the minimum order amount value is 1. It means that any discount is applied if the number of items (that meet the rules) inside the cart is superior or equal to 1.

Example: Discount is applied if 4 or more items with the Intel Core processor are in the cart.
![Threshold](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Discount/Discount+Conditions:+Reference+Information/threshold.png)

**More Advanced Example**

To create a discount that will have an extensive number of conditions, you use the condition **groups**. Meaning you collect different rules under different groups and split them into separate chunks.
Let's say you have received a task to create a discount with the following conditions:

**B2B Scenario**

The discount is going to be applied if one of the following is fulfilled:
* The price mode is **Gross**, and the subtotal amount is greater or equal: 100 € (Euro) **OR** 115 CHF (Swiss Franc)

**OR**

* The price mode is **Net**, and the subtotal amount is greater or equal: 80 € (Euro) **OR** 95 CHF (Swiss Franc)

The setup will look like the following:
![B2B scenario](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Discount/Discount+Conditions:+Reference+Information/b2b-scenario.png)

**B2C Scenario**

The discount is going to be applied if one of the following is fulfilled:
* On **Tuesday**, and the item color is red, this item does not have the label **New**, and the customer adds at least two items (or more) to a cart.

**OR**

* On **Thursday**, and the item color is white, this item does not have the label **New**, and the customer adds at least two items (or more) to a cart.

The setup will look like the following:
![B2C scenario](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Discount/Discount+Conditions:+Reference+Information/b2c-scenario.png)

#### <a name="voucher-code"></a>Voucher code tab

This section describes the information that you need to know when working with voucher codes in the *Voucher code* tab.

You enter and select the following attributes in **Edit Discount** > **Voucher code**:

| ATTRIBUTE | DESCRIPTION |  
| --- | --- |
| Quantity | Number of vouchers you need to generate. |  
| Custom code | When generating a single voucher code, you can enter it manually. If you want to create multiple codes at once, add a "Random Generated Code Length" to the custom code.|  
| Add Random Generated Code Length | This value defines the number of random characters to be added to the custom code. If you do not add any custom value, you can just select this value. The system will generate the codes with the length you select. |  
| Max number of uses (0 = Infinite usage) | Defines the maximum number of times a voucher code can be redeemed in a cart. |  

Use the placeholder **[code]** to indicate the position you want random characters to be added to.

**For example:**
   * **123[code]** (the randomly generated code will be added right after the custom code).
   * **[code]123** (the randomly generated code will be added in front of the custom code).

**Maximum number of uses**

| VALUE | BEHAVIOR |  
| --- | --- |
| 0 | Infinitely redeemable. |  
| 1 | Voucher can be redeemed once. |  
| n > 1 | Voucher can be redeemed *n* times. |  

![Voucher code](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Discount/Voucher+Codes:+Reference+Information/voucher-code.png)

**Voucher Code Pool**

The voucher codes of a discount are all contained in the same voucher code pool. One customer may only redeem one voucher code per pool per cart.

#### <a name="token-description-tables"></a>Token description tables

This section contains a set of tables that describe fields, value types, and operators you use when building a plain query.

**Tokens**

![Token](https://spryker.s3.eu-central-1.amazonaws.com/docs/User+Guides/Back+Office+User+Guides/Discount/Token+Description+Tables/tokens.png)

| VALUE | DESCRIPTION |
| --- | --- |
| Fields | The available fields may include SKU, item-price, item-quantity, or a variety of attributes (for example, **currency** on the image above). |
| Operator | Operator compares the value of a field on the left with the value(s) on the right (for example, equals (=), greater than (>)). If the expression evaluates to true, the discount can be applied (operator is **equal** on the preceding image). |
| Value | Value types must match the selected field. The asterisk (*) matches all possible values (on the preceding image, the value is **Swiss Franc**).|
| Combine Conditions | 'AND' and 'OR' operators are used to combine conditions (**AND** on the preceding image). |
|Grouping | When building more complex queries, conditions may be grouped inside parentheses '( )'. Because discount calculations and conditions are applied per item, it is not possible to use groups with ‘AND’ where each group contains at least one SKU-based rule. |

**Fields and value types (Plain Query)**

|FIELD|PLAIN QUERY|VALUE TYPE|DESCRIPTION|
|-|-|-|-|
|Calendar week|calender-week|Number|Week number in a year (1-52)|
|Day of week|day-of-week|Number|Day of week (1-7).|
|Grand total|grand-total|Number (Decimal)|Sum of all totals.|
|Subtotal|sub-total|Number (Decimal)|Sum of item prices w/o shipment expenses and discounts.|
|Item price|item-price|Number (Decimal)|Price of one item.|
|Item quantity|item-quantity|Number|Number of items.|
|Month|month|Number|Month of the year (1-12)|
|SKU|sku|String|Any value depends on how SKUs are stored.|
|Time|time|hour:minute|Time of the day.|
|Total quantity|total-quantity|Number|Total cart quantity.|
|Attribute|attribute.*|String, number|Any value.|
|Customer Group|customer-group|String|Any value, use a customer group name for an exact match.|
| Category | category | String | Any product category or sub-category. Includes any sub-categories that fall within its navigation tree.  |

**Operators (Plain Query)**

|OPERATOR|OPERATOR FOR PLAIN QUERY|VALUE TYPE|DESCRIPTION|
|-|-|-|-|
|Contains|CONTAINS|String, Number|Checks if the value is contained in the field.|
|Doesn't contain|DOES NOT CONTAIN|String, Number | Checks if the value is not contained in the field.|
|Equal|=|String, Number|Checks if the value is equal to the value of the right operand.|
|Not Equal|!=|String, Number|Checks if the value is not equal to the value of the right operand.|
|In|IS IN|List|Values need to be semicolon-separated.|
|Not In|IS NOT IN|List|Values need to be semicolon-separated.|
|Less|<|Number|Checks if the value is less than the value of the right operand.|
|Less or equal|<=|Number|Checks if the value is less than or equal to the value of the right operand.|
|Greater|>|Number|Checks if the value is greater than the value of the right operand.|
|Greater or equal|>=|Number|Checks if the value is greater than or equal to the value of the right operand.|

**What's next?**

See [Managing Discounts](/docs/scos/user/back-office-user-guides/{{page.version}}/merchandising/discount/managing-discounts.html) to learn more about the actions you can do once the discount is created.
