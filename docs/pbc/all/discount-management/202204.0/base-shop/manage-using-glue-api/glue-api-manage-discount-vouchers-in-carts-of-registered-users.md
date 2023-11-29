---
title: "Glue API: Manage discount vouchers in carts of registered users"
description: Learn how to manage discount vouchers in carts of registered users via Glue API.
last_updated: Jun 16, 2021
template: glue-api-storefront-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/managing-discount-vouchers-in-carts-of-registered-users
originalArticleId: fdd347a8-d5ae-4799-87f5-b4030c57cdec
redirect_from:
  - /2021080/docs/managing-discount-vouchers-in-carts-of-registered-users
  - /2021080/docs/en/managing-discount-vouchers-in-carts-of-registered-users
  - /docs/managing-discount-vouchers-in-carts-of-registered-users
  - /docs/en/managing-discount-vouchers-in-carts-of-registered-users
  - /docs/scos/dev/glue-api-guides/202204.0/managing-carts/carts-of-registered-users/managing-discount-vouchers-in-carts-of-registered-users.html
related:
  - title: Manage carts of registered users
    link: docs/pbc/all/cart-and-checkout/page.version/base-shop/manage-using-glue-api/manage-carts-of-registered-users/glue-api-manage-carts-of-registered-users.html
  - title: Manage items in carts of registered users
    link: docs/scos/dev/glue-api-guides/page.version/managing-carts/carts-of-registered-users/managing-items-in-carts-of-registered-users.html
---

This endpoint allows managing discount vouchers in carts of registered users.

## Installation

For detailed information on the modules that provide the API functionality and related installation instructions, see [GLUE: Promotions & Discounts feature integration](/docs/scos/dev/feature-integration-guides/{{site.version}}/glue-api/glue-api-promotions-and-discounts-feature-integration.html).

## Apply a discount voucher to a cart of a registered user

To apply a discount voucher to a cart of a registered user, send the request:

***
`POST`**/carts/*{% raw %}{{{% endraw %}uuid{% raw %}}}{% endraw %}*/vouchers**
***

| PATH PARAMETER | DESCRIPTION |
| --- | --- |
| ***{% raw %}{{{% endraw %}uuid{% raw %}}}{% endraw %}*** | The unique ID of the cart to apply the discount voucher to. To get it, [Create a cart](/docs/pbc/all/cart-and-checkout/{{page.version}}/base-shop/manage-using-glue-api/manage-carts-of-registered-users/glue-api-manage-carts-of-registered-users.html#create-a-cart) or [Retrieve a registered user's carts](/docs/pbc/all/cart-and-checkout/{{page.version}}/base-shop/manage-using-glue-api/manage-carts-of-registered-users/glue-api-manage-carts-of-registered-users.html#retrieve-registered-users-carts).  |

### Request

| HEADER KEY | HEADER TYPE | REQUIRED | DESCRIPTION |
| --- | --- | --- | --- |
| Authorization | String | &check; | An alphanumeric string that authorizes the customer to send requests to protected resources. Get it by [authenticating as a customer](/docs/pbc/all/identity-access-management/{{site.version}}/manage-using-glue-api/glue-api-authenticate-as-a-customer.html).  |

| QUERY PARAMETER | DESCRIPTION | POSSIBLE VALUES |
| --- | --- | --- |
| Include | Adds resource relationships to the request.	 | vouchers |

<details>
<summary markdown='span'>Request sample: apply a discount voucher to a cart of a registered user</summary>

`POST https://glue.mysprykershop.com/carts/1ce91011-8d60-59ef-9fe0-4493ef3628b2/vouchers`

```json
{
    "data": {
        "type": "vouchers",
        "attributes": {
            "code": "sprykerku2f"
        }
    }
}
```
</details>

<details>
<summary markdown='span'>Request sample: apply a discount voucher to a cart of a registered user with details on discount voucher information</summary>

`POST https://glue.mysprykershop.com/carts/1ce91011-8d60-59ef-9fe0-4493ef3628b2/vouchers?include=vouchers`

```json
{
    "data": {
        "type": "vouchers",
        "attributes": {
            "code": "mydiscount-qa1ma"
        }
    }
}
```
</details>

| ATTRIBUTE | TYPE | REQUIRED | DESCRIPTION |
| --- | --- | --- | --- |
| code | String | yes | The unique ID of a discount voucher to apply.  |

### Response

<details>
<summary markdown='span'>Response sample: apply a discount voucher to a cart of a registered user</summary>

```json
{
    "data": {
        "type": "carts",
        "id": "c9310692-2ab0-5edc-bb41-fee6aa828d55",
        "attributes": {
            "priceMode": "GROSS_MODE",
            "currency": "EUR",
            "store": "DE",
            "totals": {
                "expenseTotal": 0,
                "discountTotal": 21831,
                "taxTotal": 19752,
                "subtotal": 145540,
                "grandTotal": 123709,
                "priceToPay": 123709
            },
            "discounts": [
                {
                    "displayName": "5% discount on all white products",
                    "amount": 7277,
                    "code": null
                }
            ],
            "thresholds": []
        },
        "links": {
            "self": "https://glue.mysprykershop.com/carts/c9310692-2ab0-5edc-bb41-fee6aa828d55"
        }
    }
}
```
</details>

<details>
<summary markdown='span'>Response sample: apply a discount voucher to a cart of a registered user with details on discount voucher information</summary>

```json
{
    "data": {
        "type": "carts",
        "id": "56a0b4e4-21d8-516f-acd5-90581c996676",
        "attributes": {
            "priceMode": "GROSS_MODE",
            "currency": "EUR",
            "store": "DE",
            "name": "Shopping cart",
            "isDefault": true,
            "totals": {...},
            "discounts": [
                {
                    "displayName": "My Discount",
                    "amount": 83133,
                    "code": null
                },
                {
                    "displayName": "10% Discount for all orders above",
                    "amount": 33253,
                    "code": null
                }
            ],
            "thresholds": []
        },
        "links": {...},
        "relationships": {
            "vouchers": {
                "data": [
                    {
                        "type": "vouchers",
                        "id": "mydiscount-qa1ma"
                    }
                ]
            }
        }
    },
    "included": [
        {
            "type": "vouchers",
            "id": "mydiscount-qa1ma",
            "attributes": {
                "amount": 83133,
                "code": "mydiscount-qa1ma",
                "discountType": "voucher",
                "displayName": "My Discount",
                "isExclusive": false,
                "expirationDateTime": "2020-02-29 00:00:00.000000",
                "discountPromotionAbstractSku": null,
                "discountPromotionQuantity": null
            },
            "links": {
                "self": "https://glue.mysprykershop.com/vouchers/mydiscount-qa1ma?include=vouchers"
            }
        }
    ]
}
```
</details>

| INCLUDED RESOURCE | ATTRIBUTE | TYPE | DESCRIPTION |
| --- | --- | --- | --- |
| vouchers | displayName | String | The discount name displayed on the Storefront. |
| vouchers | amount | Integer | The amount of the provided discount. |
| vouchers | code | String | The discount code. |
| vouchers | discountType | String | The discount type. |
| vouchers | isExclusive | Boolean | If true, the discount is exclusive. |
| vouchers | expirationDateTime | DateTimeUtc | The date and time on which the discount expires. |
| vouchers | discountPromotionAbstractSku | String | The SKU of the products to which the discount applies. If the discount can be applied to any product, the value is `null`. |
| vouchers | discountPromotionQuantity | Integer | Specifies the amount of the product required to be able to apply the discount. If the minimum number is `0`, the value is `null`. |

## Remove a discount voucher from a registered user's cart

To remove a discount voucher, send the request:

***
`DELETE`**/carts/*{% raw %}{{{% endraw %}uuid{% raw %}}}{% endraw %}*/vouchers/*{% raw %}{{{% endraw %}voucher_id{% raw %}}}{% endraw %}***
***

| PATH PARAMETER | DESCRIPTION |
| --- | --- |
| ***{% raw %}{{{% endraw %}uuid{% raw %}}}{% endraw %}*** | The unique ID of the registered user's cart to remove the discount voucher from. To get it, [Retrieve a registered user's cart](/docs/pbc/all/cart-and-checkout/{{page.version}}/base-shop/manage-using-glue-api/manage-carts-of-registered-users/glue-api-manage-carts-of-registered-users.html#retrieve-registered-users-carts).  |
| ***{% raw %}{{{% endraw %}voucher_id{% raw %}}}{% endraw %}*** | The unique ID of the voucher to remove. To get it, [Retrieve a registered user's cart](/docs/pbc/all/cart-and-checkout/{{page.version}}/base-shop/manage-using-glue-api/manage-carts-of-registered-users/glue-api-manage-carts-of-registered-users.html#retrieve-a-registered-users-cart) or [Retrieve a registered user's carts](/docs/pbc/all/cart-and-checkout/{{page.version}}/base-shop/manage-using-glue-api/manage-carts-of-registered-users/glue-api-manage-carts-of-registered-users.html#retrieve-registered-users-carts) with the `vouchers` resource included.  |

### Request

| HEADER KEY | HEADER TYPE | REQUIRED | DESCRIPTION |
| --- | --- | --- | --- |
| Authorization | String | &check; | An alphanumeric string that authorizes the customer to send requests to protected resources. Get it by [authenticating as a customer](/docs/pbc/all/identity-access-management/{{site.version}}/manage-using-glue-api/glue-api-authenticate-as-a-customer.html).  |

Request sample: remove a discount voucher from a registered user's cart

`DELETE https://glue.mysprykershop.com/carts/1ce91011-8d60-59ef-9fe0-4493ef3628b2/vouchers/mydiscount-we3ca`

### Response

If the voucher is deleted successfully, the endpoints returns the `204 No Data` status code.

## Possible errors

| CODE | REASON |
| --- | --- |
| 001 | Access token is incorrect. |
| 002 | Access token is missing. |
| 003 | Failed to log in the user. |
| 3301 | Cart or voucher with the specified ID is not found. |
| 3302 | Incorrect voucher code or the voucher cannot be applied. |
| 3303 | Cart code can't be removed. |

To view generic errors that originate from the Glue Application, see [Reference information: GlueApplication errors](/docs/scos/dev/glue-api-guides/{{page.version}}/reference-information-glueapplication-errors.html).
