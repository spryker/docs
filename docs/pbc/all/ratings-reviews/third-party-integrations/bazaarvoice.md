---
title: Bazaarvoice
description: Find out how you can integrate and use Bazaarvoice in your Spryker shop
template: howto-guide-template
redirect_from:
   - docs/aop/user/apps/bazaarvoice.html
   - docs/acp/user/apps/bazaarvoice.html  
---

The [Bazaarvoice](https://www.bazaarvoice.com/?ref=spryker-documentation) app lets you collect and add user-generated content (UGC) to your product pages. 

The Bazaarvoice service offers the following UGC: 

- [Rating summaries](https://knowledge.bazaarvoice.com/wp-content/conversations/en_US/Display/display_integration.html#rating-summary?ref=spryker-documentation), or star ratings
- [Product reviews](https://knowledge.bazaarvoice.com/wp-content/conversations/en_US/Display/display_integration.html#reviews?ref=spryker-documentation)  
<!---- [Questions and answers](https://knowledge.bazaarvoice.com/wp-content/conversations/en_US/Display/display_integration.html#questions--answers)-->

Bazaarvoice uses the content syndication approach, which means that stores using Bazaarvoice republish each others' content. For example, if a store within the Bazaarvoice's network has got a new product review, this review is shared across all other stores in the network that also have this product.

{% info_block warningBox "Important" %}

To enable Bazaarvoice to match your products to products in other stores and upload product reviews into your store, you must use UPCs or EANs as unique identifiers for your products.

{% endinfo_block %}

When you connect Bazaarvoice, the app puts JavaScrip tags into your store, and the JavaScript code tells the app where to insert the Bazaarvoice content—reviews, star ratings, or questions and answers.

{% info_block infoBox "Info" %}

If you have Bazaarvoice integrated, the Spryker default [Product Ratings and Reviews feature](/docs/scos/user/features/{{site.version}}/product-rating-and-reviews-feature-overview.html) is turned off. This means that ratings and reviews collected with the default Spryker Product Ratings and Reviews feature are replaced with the BazzareVoice ratings and reviews.

{% endinfo_block %}

## Prerequisites to use Bazaarvoice in your project

The BazaarVoice app requires the following Spryker modules:

* `spryker/asset: ^1.2.0`
* `spryker/asset-storage: ^1.1.0`
* `spryker/message-broker: ^1.0.0`
* `spryker/message-broker-aws: ^1.0.0`
* `spryker/message-broker-extension: ^1.0.0`
* `spryker-shop/asset-widget: ^1.0.0`
* `spryker-shop/product-detail-page: ^3.17.0`
* `spryker-shop/product-category-widget: ^1.6.0`
* `spryker-shop/shop-ui: ^1.59.0`
