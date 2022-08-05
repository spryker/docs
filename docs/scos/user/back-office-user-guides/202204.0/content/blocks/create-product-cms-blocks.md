---
title: Create product CMS blocks
description: Learn how to create product CMS blocks in the Back Office.
last_updated: June 2, 2022
template: back-office-user-guide-template
related:
  - title: Edit CMS blocks
    link: docs/scos/user/back-office-user-guides/page.version/content/blocks/edit-cms-blocks.html
---

## Prerequisites

* [Integrate product CMS blocks](/docs/scos/dev/technical-enhancement-integration-guides/integrate-product-cms-blocks.html).

* Create the abstract products whose pages you want to show the block on. For instructions, see [Create abstract products](/docs/scos/user/back-office-user-guides/{{page.version}}/catalog/products/manage-abstract-products-and-product-bundles/create-abstract-products-and-product-bundles.html).

* Review the [reference information](#reference-information-create-product-cms-blocks) before you start, or look up the necessary information as you go through the process.

## Create a product CMS block

1. Go to **Content&nbsp;<span aria-label="and then">></span> Blocks**.
2. On the **Overview of CMS Blocks** page, click  **Create block**.
    This opens the **Create new CMS Block** page.
3. For **STORE RELATION**, select the stores you want the CMS block to be displayed in.
4. For **TEMPLATE**, select **Product Block**.
5. Enter a **NAME**.
6. Optional: Select a **VALID FROM** date.
7. Optional: Select a **VALID TO** date.  
8. Optional: Enter and select one or more **PRODUCTS**.
9. Click **Save**.
    This opens the **Edit CMS Block Glossary** page with a success message displayed.
10. Optional: For **CONTENT**, add content to the block per placeholder per locale.
11. Click **Save**.
    This opens the **Edit Block Glossary** page with a success message displayed.



## Reference information: Create product CMS blocks

| ATTRIBUTE  | DESCRIPTION |
| --- | --- |
| STORE RELATION |  Stores to display the block in. |
| TEMPLATE | Defines the layout of the CMS Block. A developer can [create more templates](/docs/scos/dev/tutorials-and-howtos/howtos/feature-howtos/cms/howto-create-cms-templates.html#cms-block-template). |
| NAME | You will use this name when [assigning the block to a slot in a page](/docs/scos/user/back-office-user-guides/{{page.version}}/content/slots/managing-slots.html#assigning-cms-blocks-to-slots). |
| VALID FROM and VALID TO | Dates that inclusively specify when the block is to be visible on the Storefront. |
| PRODUCTS | The block will be displayed on the product details pages of these products. |


## Reference information: Add content to the placeholders of a CMS block

{% include scos/user/back-office-user-guides/content/blocks/reference-information-add-content-to-the-placeholders-of-a-cms-block.md %} <!-- To edit, see /_includes/scos/user/back-office-user-guides/content/blocks/reference-information-add-content-to-the-placeholders-of-a-cms-block.md -->


## Next steps

[Edit CMS blocks](/docs/scos/user/back-office-user-guides/{{page.version}}/content/blocks/edit-cms-blocks.html)
