---
title: Managing filter preferences
description: Use the procedure to reorder filters, specify a filter type and add translations to the filter name in the Back Office.
last_updated: Aug 2, 2021
template: back-office-user-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/managing-filter-preferences
originalArticleId: a12072b2-b53e-4cf6-8ef1-f94c08cdc6ef
redirect_from:
  - /2021080/docs/managing-filter-preferences
  - /2021080/docs/en/managing-filter-preferences
  - /docs/managing-filter-preferences
  - /docs/en/managing-filter-preferences
related:
  - title: Managing Search Preferences
    link: docs/scos/user/back-office-user-guides/page.version/merchandising/search-and-filters/managing-search-preferences.html
---

This article describes how to manage filter preferences.

To start working with the filter preferences, navigate to the **Merchandising** > **Filter Settings** section.

## Prerequisites

Make sure that the attribute you are going to create a filter preference for is created and assigned to a product.

## Creating filter preferences

To create a filter preference:
1. In the top right corner of the *Filter preferences* page, click **Create filter**.
2. On the *Create filter* page, do the following:
    1. Enter the attribute key to the respective field. The attribute key can be found in **Product Attributes > Attributes Key** of a specific attribute.
    2. In the **Filter Type** drop-down, select either multi-select or range.
    3. Enter the translations for all locations set up in your store.
3. Click **Save**.

**Tips & tricks**
- The filter is created by it will not be available for use unless you synchronize the filter preferences.
To do the synchronization, in the top right corner of the *Filter Preferences* page, click **Synchronize filter preference**
- There is no way to specify specific categories when creating filters. If, however, products within a category do not contain values for the attribute to which the filter is assigned, the filter does not appear on the Storefront. For example, if you created a category filter, it is assigned to all of the default categories.  However, it only appears for those products on the Storefront that have attributes that this category filter has.

## Editing filter preferences

To edit a filter preference:
1. In the _Actions_ column of the *Filter preferences* table, click **Edit** for the filter you need to update.
2. Update the needed values.
    **Attribute key** is greyed out and is not available for modifications.
 3. Click **Save**.
 4. On the *View filter* page, in the top right corner, click **List of filters**.
 5. On the *Filter preferences* page, click **Synchronize filter preferences**.

## Viewing and deleting filter preferences

 *To view a filter*, click **View** in the _Actions_ column for a specific filter.

To delete a filter:
 1. in the _Actions_ column, click **Delete**  for a specific filter.
 **OR**
2. In the top right corner of the page while viewing a filter, click **Delete**.

**What's next?**
<br>Once the filter preference is created, you can use it in the **Category Filters** section. That is done to enable specific category(s) to which the product with this attribute is assigned, to be filtered based on this specific filter.

See [Managing category filters](/docs/scos/user/back-office-user-guides/{{page.version}}/merchandising/search-and-filters/managing-category-filters.html) to know how to set up the category filters.
