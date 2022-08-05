---
title: Retrieve discounts in customer carts
description: Learn how to retrieve cart rules, vouchers, and promotional items in customer carts via Glue API.
last_updated: Jul 25, 2022
template: glue-api-storefront-guide-template
---

This document describes how to retrieve cart rules, vouchers, and promotional items in customer carts. To learn how to retrieve all information about customer carts, see [Retrieving customer carts](https://docs.spryker.com/docs/scos/dev/glue-api-guides/{{site.version}}/managing-customers/retrieving-customer-carts.html).

## Installation

For details on the modules that provide the API functionality and how to install them, see the following docs:
* [Glue API: Cart feature integration](/docs/scos/dev/feature-integration-guides/{{site.version}}/glue-api/glue-api-cart-feature-integration.html)
* [Glue API: Promotions & Discounts feature integration](/docs/scos/dev/feature-integration-guides/{{site.version}}/glue-api/glue-api-promotions-and-discounts-feature-integration.html)


## Retrieve customer’s carts

To retrieve a customer’s carts, send the following request:

`GET` **/customers/*{% raw %}{{{% endraw %}customerId{% raw %}}}{% endraw %}*/carts**

{% info_block infoBox "Note" %}

Alternatively, you can retrieve all carts belonging to a customer through the **/carts** endpoint. For details, see [Retrieve discounts in carts of registered users](/docs/scos/dev/glue-api-guides/{{site.version}}/managing-carts/carts-of-registered-users/managing-carts-of-registered-users.html#retrieve-registered-users-carts).

{% endinfo_block %}


| PATH PARAMETER | DESCRIPTION |
|-|-|
| ***{% raw %}{{{% endraw %}customerId{% raw %}}}{% endraw %}*** | Customer unique identifier to retrieve carts of. To get it, [retrieve a customer](/docs/scos/dev/glue-api-guides/{{site.version}}/managing-customers/managing-customers.html#retrieve-customers) or [create a customer](/docs/scos/dev/glue-api-guides/{{site.version}}/managing-customers/managing-customers.html#create-a-customer). |

### Request

| HEADER KEY | HEADER VALUE | REQUIRED | DESCRIPTION |
|-|-|-|-|
| Authorization | string | &check; | Alphanumeric string that authorizes the customer to send requests to protected resources. Get it by [authenticating as a customer](/docs/scos/dev/glue-api-guides/{{site.version}}/managing-customers/authenticating-as-a-customer.html). |

| QUERY PARAMETER | DESCRIPTION | EXEMPLARY VALUES |
|-|-|-|
| include | Adds resource relationships to the request. |  <ul><li>cart-rules</li><li>promotional-items</li><li>vouchers</li></ul>  |



| REQUEST | USAGE |
|-|-|
| GET https://glue.mysprykershop.com/customers/DE--1/?include=cart-rules | Retrieve all carts of a user with cart rules. |
| GET https://glue.mysprykershop.com/customers/DE--1/?include=vouchers | Retrieve all carts of a user with information about applied vouchers. |
| GET https://glue.mysprykershop.com/customers/DE--1/?include=promotional-items | Retrieve information about promotional items for the cart. |

### Response

<details><summary markdown='span'>Response sample: retrieve customer's carts with the cart rules included</summary>

```json
{
    "data": [
        {
            "type": "carts",
            "id": "59743e37-0182-5153-9935-77106741a9d2",
            "attributes": {
                "priceMode": "GROSS_MODE",
                "currency": "EUR",
                "store": "DE",
                "name": "Purchases",
                "isDefault": true,
                "totals": {
                    "expenseTotal": null,
                    "discountTotal": null,
                    "taxTotal": null,
                    "subtotal": null,
                    "grandTotal": null
                },
                "discounts": []
            },
            "links": {
                "self": "https://glue.mysprykershop.com/carts/59743e37-0182-5153-9935-77106741a9d2"
            }
        },
        {
            "type": "carts",
            "id": "2fd32609-b6b0-5993-9254-8d2f271941e4",
            "attributes": {
                "priceMode": "GROSS_MODE",
                "currency": "EUR",
                "store": "DE",
                "name": "My Cart",
                "isDefault": false,
                "totals": {
                    "expenseTotal": 0,
                    "discountTotal": 2965,
                    "taxTotal": 4261,
                    "subtotal": 29651,
                    "grandTotal": 26686
                },
                "discounts": [
                    {
                        "displayName": "10% Discount for all orders above",
                        "amount": 2965,
                        "code": null
                    }
                ]
            },
            "links": {
                "self": "https://glue.mysprykershop.com/carts/2fd32609-b6b0-5993-9254-8d2f271941e4"
            },
            "relationships": {
                "cart-rules": {
                    "data": [
                        {
                            "type": "cart-rules",
                            "id": "1"
                        }
                    ]
                }
            }
        },
        {
            "type": "carts",
            "id": "2b72635a-9363-56f5-9ba7-55631b8ad71e",
            "attributes": {
                "priceMode": "GROSS_MODE",
                "currency": "EUR",
                "store": "DE",
                "name": "New",
                "isDefault": false,
                "totals": {
                    "expenseTotal": 0,
                    "discountTotal": 10206,
                    "taxTotal": 14666,
                    "subtotal": 102063,
                    "grandTotal": 91857
                },
                "discounts": [
                    {
                        "displayName": "10% Discount for all orders above",
                        "amount": 10206,
                        "code": null
                    }
                ]
            },
            "links": {
                "self": "https://glue.mysprykershop.com/carts/2b72635a-9363-56f5-9ba7-55631b8ad71e"
            },
            "relationships": {
                "cart-rules": {
                    "data": [
                        {
                            "type": "cart-rules",
                            "id": "1"
                        }
                    ]
                }
            }
        }
    ],
    "links": {
        "self": "https://glue.mysprykershop.com/carts?include=cart-rules"
    },
    "included": [
        {
            "type": "cart-rules",
            "id": "1",
            "attributes": {
                "amount": 10206,
                "code": null,
                "discountType": "cart_rule",
                "displayName": "10% Discount for all orders above",
                "isExclusive": false,
                "expirationDateTime": "2020-12-31 00:00:00.000000",
                "discountPromotionAbstractSku": null,
                "discountPromotionQuantity": null
            },
            "links": {
                "self": "https://glue.mysprykershop.com/cart-rules/1"
            }
        }
    ]
}
```
</details>

<details><summary markdown='span'>Response sample: retrieve customer's carts with the information on vouchers included</summary>

```json
{
    "data": [
        {
            "type": "carts",
            "id": "976af32f-80f6-5f69-878f-4ea549ee0830",
            "attributes": {
                "priceMode": "GROSS_MODE",
                "currency": "EUR",
                "store": "DE",
                "totals": {
                    "expenseTotal": 0,
                    "discountTotal": 1663,
                    "taxTotal": 5046,
                    "subtotal": 33265,
                    "grandTotal": 31602,
                    "priceToPay": 31602
                },
                "discounts": [
                    {
                        "displayName": "5% discount on all white products",
                        "amount": 1663,
                        "code": null
                    }
                ]
            },
            "links": {
                "self": "https://glue.mysprykershop.com/carts/976af32f-80f6-5f69-878f-4ea549ee0830?include=vouchers"
            },
            "relationships": {
                "vouchers": {
                    "data": [
                        {
                            "type": "vouchers",
                            "id": "sprykerya1y"
                        }
                    ]
                }
            }
        }
    ],
    "links": {
        "self": "https://glue.mysprykershop.com/carts?include=vouchers"
    },
    "included": [
        {
            "type": "vouchers",
            "id": "sprykerya1y",
            "attributes": {
                "amount": 1663,
                "code": "sprykerya1y",
                "discountType": "voucher",
                "displayName": "5% discount on all white products",
                "isExclusive": false,
                "expirationDateTime": "2021-02-28 00:00:00.000000",
                "discountPromotionAbstractSku": null,
                "discountPromotionQuantity": null
            },
            "links": {
                "self": "https://glue.mysprykershop.com/carts/976af32f-80f6-5f69-878f-4ea549ee0830/cart-codes/sprykerya1y"
            }
        }
    ]
}
```
</details>

<details><summary markdown='span'>Response sample: retrieve customer's carts withe the information on  promotional items included</summary>

```json
{
    "data": [
        {
            "type": "carts",
            "id": "e877356a-5d8f-575e-aacc-c790eeb20a27",
            "attributes": {
                "priceMode": "GROSS_MODE",
                "currency": "EUR",
                "store": "DE",
                "name": "Everyday purchases",
                "isDefault": true,
                "totals": {
                    "expenseTotal": 0,
                    "discountTotal": 17352,
                    "taxTotal": 19408,
                    "subtotal": 173517,
                    "grandTotal": 156165,
                    "priceToPay": 56165
                },
                "discounts": [
                    {
                        "displayName": "10% Discount for all orders above",
                        "amount": 17352,
                        "code": null
                    }
                ]
            },
            "links": {
                "self": "https://glue.mysprykershop.com/carts/e877356a-5d8f-575e-aacc-c790eeb20a27"
            },
            "relationships": {
                "promotional-items": {
                    "data": [
                        {
                            "type": "promotional-items",
                            "id": "bfc600e1-5bf1-50eb-a9f5-a37deb796f8a"
                        }
                    ]
                }
            }
        }
    ],
    "links": {
        "self": "https://glue.mysprykershop.com/carts?include=promotional-items"
    },
    "included": [
        {
            "type": "promotional-items",
            "id": "bfc600e1-5bf1-50eb-a9f5-a37deb796f8a",
            "attributes": {
                "sku": "112",
                "quantity": 2
            },
            "links": {
                "self": "https://glue.mysprykershop.com/promotional-items/bfc600e1-5bf1-50eb-a9f5-a37deb796f8a"
            }
        }
    ]
}
```
</details>


{% include pbc/all/glue-api-guides/retrieve-customer-carts-response-attributes.md %} <!-- To edit, see /_includes/pbc/all/glue-api-guides/retrieve-customer-carts-response-attributes.md -->

| INCLUDED RESOURCE | ATTRIBUTE | TYPE | DESCRIPTION |
|-|-|-|-|
| promotional-items | id | String | Unique identifier of the promotional item. The ID can be used to apply the promotion to the given purchase. |
| promotional-items | sku | String | SKU of the promoted abstract product. |
| promotional-items | quantity | Integer | Specifies how many promotions can be applied to the given purchase. |
| product-options | optionGroupName | String | Name of the group to which the option belongs. |
| product-options | sku | String | SKU of the product option. |
| product-options | optionName | String | Product option name. |
| product-options | price | Integer | Product option price in cents. |
| product-options | currencyIsoCode | String | ISO 4217 code of the currency in which the product option price is specified. |
| vouchers, cart-rules | displayName | String | Discount name displayed on the Storefront. |
| vouchers, cart-rules | amount | Integer | Amount of the provided discount. |
| vouchers, cart-rules | code | String | Discount code. |
| vouchers, cart-rules | discountType | String | Discount type. |
| vouchers, cart-rules | isExclusive | Boolean | Discount exclusivity. |
| vouchers, cart-rules | expirationDateTime | DateTimeUtc | Date and time on which the discount expires. |
| vouchers, cart-rules | discountPromotionAbstractSku | String | SKU of the products to which the discount applies. If the discount can be applied to any product, the value is `null`. |
| vouchers, cart-rules | discountPromotionQuantity | Integer | Specifies the amount of the product required to be able to apply the discount. If the minimum number is `0`, the value is `null`. |

## Possible errors

| CODE | REASON |
|-|-|
| 001 | Access token is invalid. |
| 002 | Access token is missing. |
| 402 | Customer with the specified ID was not found. |
| 802 | Request is unauthorized. |

To view generic errors that originate from the Glue Application, see [Reference information: GlueApplication errors](/docs/scos/dev/glue-api-guides/{{site.version}}/reference-information-glueapplication-errors.html).
