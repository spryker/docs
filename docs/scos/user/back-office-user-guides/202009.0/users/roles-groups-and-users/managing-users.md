---
title: Managing users
description: The procedures help create, edit, activate/deactivate or delete Back Office users, set a language to the Back Office user account, and make a user be an agent.
template: back-office-user-guide-template
originalLink: https://documentation.spryker.com/v6/docs/managing-users
originalArticleId: affe5aa9-c60e-4e7b-86dc-127e90d49473
redirect_from:
  - /v6/docs/managing-users
  - /v6/docs/en/managing-users
related:
  - title: User and Rights Management
    link: docs/scos/dev/feature-walkthroughs/page.version/customer-account-management-feature-walkthrough/user-and-rights-overview.html
---

This topic describes how to manage users.

To start managing users, go to **Users** > **Users**.

You can do the following:
* Create a new user record
* Assign customers to a specific user
* Edit a user
* Deactivate/activate a user
* Delete a user from the system

## Creating users

You have already done the primary setup (you have created a [role](/docs/scos/user/back-office-user-guides/{{page.version}}/users/roles-groups-and-users/managing-roles.html) and [group](/docs/scos/user/back-office-user-guides/{{page.version}}/users/roles-groups-and-users/managing-groups.html)), so now it is time to add an actual user record to the system.

**To create a user record**:
1. Click **Add New User** in the top right corner of the **User** page.
2. Enter and select the following attributes:

    * E-mail, Password, Repeat Password
    * First Name and Last Name
    * Assigned groups
    * Agent
    * Interface language

{% info_block infoBox %}

 See [User: Reference Information](/docs/scos/user/back-office-user-guides/{{page.version}}/users/roles-groups-and-users/references/reference-information-user.html) for details on these attributes.

{% endinfo_block %}       
3. Click **Create**.

That's it. The created user record appears on the *Users* page.    

**Tips & tricks**
There is a way to initiate a create-new-user flow while editing a user record. To do that, on the **Edit User** page, click **Add User** in the top right corner.


## Assigning customers to users
The *Assign Customers* option is used to assign store customers' records to the Back office user records. This is done to enable the Back Office user to preview the CMS Pages in the online store (see [CMS Pages](/docs/scos/user/back-office-user-guides/{{page.version}}/content/pages/managing-cms-pages.html#previewing-cms-pages) set of topics).

**To assign a customer**:
1. Navigate to the **Users** page.
2. In the **Users List > Action** column, select **Assign Customers**.
3. In the **List of customers > Select customers to assign** table, select the check-box next to the customer you want to assign (multiple customers can be selected).
4. Click **Save**.
{% info_block infoBox %}

A customer cannot be assigned to multiple users at a time.

{% endinfo_block %}

**Tips & tricks**
To de-assign a customer:
1. On the **Assign Customers to User** page, scroll down to the *Assigned customer*s table.
2. Deselect the check-box next to the customer(s) that needs to become unassigned, and click **Save**.


## Editing a user
**To edit a user:**
1. In **Users List > Action** column, click **Edit**  if you want to change user's details. See [User: Reference Information](/docs/scos/user/back-office-user-guides/{{page.version}}/users/roles-groups-and-users/references/reference-information-user.html) for  more details.
2. When the updates are done, click **Update**.

## Activating and deactivating a user
**To activate or deactivate a user:**
1. In the **Users List > Action** column, click **Activate** (or **Deactivate**).

{% info_block infoBox %}

If a user has deactivated themselves, this user will get logged out immediately and the message about the successful deactivation will be shown.

{% endinfo_block %}

2. The status in the _Status_ column will be changed to *Active* or *Deactivated* depending on the action you performed.

 ## Deleting a user

**To delete a user:**
 1. In the **Users List > Action** column, click **Delete**.
2. On the **Warning** page, click **Delete** to confirm the action.
{% info_block infoBox %}
The user's status in the _Status_ column will change to _Deleted_, however, the user will still stay in the **Users List** table. If the user has deleted themselves, this user will get logged out immediately and the message about the successful deletion will be shown.
{% endinfo_block %}
