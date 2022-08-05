---
title: Spryker Core Back Office feature overview
description: The document provides general information about the actions you can perform in Spryker Back Office.
last_updated: Jun 16, 2021
template: concept-topic-template
originalLink: https://documentation.spryker.com/2021080/docs/the-back-office-overview
originalArticleId: 33ffb1b7-d9b5-457a-90a1-170e36479d5b
redirect_from:
  - /2021080/docs/the-back-office-overview
  - /2021080/docs/en/the-back-office-overview
  - /docs/the-back-office-overview
  - /docs/en/the-back-office-overview
  - /2021080/docs/back-office-login-overview
  - /2021080/docs/en/back-office-login-overview
  - /docs/back-office-login-overview
  - /docs/en/back-office-login-overview
  - /docs/scos/user/features/202200.0/spryker-core-back-office-feature-overview/spryker-core-back-office-feature-overview.html

---

A Spryker-based shop ships with a comprehensive, intuitive administration area and consists of numerous features that give you a strong hold over the customization of your store. Here you can tailor features to your specific needs, manage orders, products, and customers, and modify the look and feel of your store by—for example, designing eye-catching marketing campaigns and promotions, and much more.

The Spryker Back Office provides you with a variety of sections that are logically connected to each other.

{% info_block infoBox "Spryker Back Office" %}

It provides the product and content management capabilities, categories and navigation building blocks, search and filter customizations, barcode generator, order handling, company structure creation (_for B2B users_), and merchant-buyer contracts' setup.

{% endinfo_block %}

With Spryker Back Office, you can do the following:
* Manage orders placed by your customers as well as create orders for customers.
* Create and manage customers.
* Build and manage product categories.
* Create and manage CMS blocks and pages.
* Handle translations.
* Manage products and all elements related to them (availability, labels, options, types).
* Customize search and filters for the online store.
* Create and manage discounts.
* Build and manage the main navigation of your online store.
* Create new carrier companies and shipment methods as well as manage those.
* Create admin users, and add roles and user groups.

Depending on the roles and teams in your project, you can limit the access of different Back Office users to specific Back Office areas.

**Back Office provides both B2B and B2C capabilities.**

{% info_block infoBox "Info" %}

The following diagram shows what features are used for both *B2B and B2C* and which are *B2B-specific*.

{% endinfo_block %}

![B2B and B2C features](https://spryker.s3.eu-central-1.amazonaws.com/docs/scos/user/features/spryker-core-back-office-feature-overview/spryker-core-back-office-feature-overview.md/b2b-and-b2c-features.png)

You can always define what exactly is going to be needed for your specific project.

## Back Office authentication


To use the Spryker Back Office, users have to authenticate to the Back Office. They can authenticate by the following:

* Regular Back Office user account.
* Third-party sign-on (optional).

To *authenticate as a regular Back Office user*, you must have a Back Office user account. To learn how to create and manage Back Office user accounts, see [Managing users](/docs/scos/user/back-office-user-guides/{{page.version}}/users/managing-users/creating-users.html).

You can also let your users sign in from a third-party service set up for your project. The third-party sign-on uses the [OpenID](https://en.wikipedia.org/wiki/OpenID) protocol for authentication.

{% info_block infoBox %}

The feature is shipped with an exemplary ECO module that supports authentication using Microsoft Azure Active Directory. With the existing infrastructure, you can develop your own ECO modules for the identity managers you need.

{% endinfo_block %}

If a user chooses to log in using a third party, the user is redirected to the OAuth provider's sign-in page—for example, Microsoft Azure. If the user logs in to the third-party service successfully, the check is made if the user exists in the Spryker database. If the user exists in the database and is active, the user is logged in. If the user does not exist in the database, you can have one of the two different behaviors or strategies for your project:

<a name="strategies"></a>

**Strategy 1: Upon the first login, create the Back Office admin user based on the third-party system’s user data.**

If a user who does not exist in the Spryker database logs in for the first time, the following happens:
* Based on the third-party system’s user data such as first name, last name, and email, the Back Office user is created and visible on the [Users page](/docs/scos/user/back-office-user-guides/{{page.version}}/users/managing-users/creating-users.html) in the Back Office.
* The user is assigned to the default [group](/docs/scos/user/back-office-user-guides/{{page.version}}/users/managing-user-groups/creating-user-groups.html).

With Strategy 1, the login process looks like this:

![image](https://confluence-connect.gliffy.net/embed/image/5b0f6ab5-d4d5-4b53-b82a-d73bec9c81ea.png?utm_medium=live&utm_source=custom)

**Strategy 2: Do not log in to the user unless they exist in the Spryker database.**

Before a user can log in to Back Office with third-party service credentials, the user must be added and set to `Active` in the database. You can add the user using either the Back Office or the ACL module.

With Strategy 2, the login process looks like this:

![image](https://confluence-connect.gliffy.net/embed/image/5b0f6ab5-d4d5-4b53-b82a-d73bec9c81ea.png?utm_medium=live&utm_source=custom)

## Current constraints

The feature has the following functional constraint:

Each of the identity managers is an ECO module that must be developed separately. After the module development, the identity manager’s roles and permissions must be mapped to the roles and permissions in Spryker. The mapping is always implemented at the project level.


## Related Business User articles

|BACK OFFICE USER GUIDES|
|---|
| [Get a general idea of the Back Office Translations](/docs/scos/user/features/{{page.version}}/spryker-core-back-office-feature-overview/back-office-translations-overview.html) |
| **Work with the Back Office**: |
| [Log in to the Back Office](/docs/scos/user/back-office-user-guides/{{page.version}}/logging-in-to-the-back-office.html) |

{% info_block warningBox "Developer guides" %}

Are you a developer? See [Spryker Core back Office feature walkthrough](/docs/scos/dev/feature-walkthroughs/{{page.version}}/spryker-core-back-office-feature-walkthrough/spryker-core-back-office-feature-walkthrough.html) for developers.

{% endinfo_block %}
