---
title: Retrieve tax sets of abstract products
description: Retrieve general information about abstract products and related resources.
last_updated: Jun 21, 2021
template: glue-api-storefront-guide-template
---

This document describes how to retrieve tax sets of abstract products. To retrieve full information of abstract products, see [Retrieve abstract products](/docs/scos/dev/glue-api-guides/{{site.version}}/managing-products/abstract-products/retrieving-abstract-products.html).

## Installation

For detailed information on the modules that provide the API functionality and related installation instructions, see [Glue API: Products Feature Integration](/docs/scos/dev/feature-integration-guides/{{site.version}}/glue-api/glue-api-product-feature-integration.html).

## Retrieve tax sets of an abstract product

---
`GET` **/abstract-products/*{% raw %}{{{% endraw %}abstract_product_sku{% raw %}}}{% endraw %}?include=product-tax-sets***

---


| PATH PARAMETER | DESCRIPTION |
| --- | --- |
| ***{% raw %}{{{% endraw %}abstract_product_sku{% raw %}}}{% endraw %}*** | SKU of an abstract product to get information for. |

### Request


`GET https://glue.mysprykershop.com/abstract-products/001?include=product-tax-sets`:  Retrieve information about the abstract product with SKU `001` with its tax sets.



### Response




<details>
<summary markdown='span'>Response sample: retrieve information about an abstract product with the details about tax sets</summary>

```json
{
    "data": {
        "type": "abstract-products",
        "id": "001",
        "attributes": {
            "sku": "001"
        },
        "links": {
            "self": "https://glue.mysprykershop.com/abstract-products/001?include=product-tax-sets"
        },
        "relationships": {
            "product-tax-sets": {
                "data": [
                    {
                        "type": "product-tax-sets",
                        "id": "0e93b0d4-6d83-5fc1-ac1d-d6ae11690406"
                    }
                ]
            }
        }
    },
    "included": [
        {
            "type": "product-tax-sets",
            "id": "0e93b0d4-6d83-5fc1-ac1d-d6ae11690406",
            "attributes": {
                "name": "Entertainment Electronics",
                "restTaxRates": [
                    {
                        "name": "Austria Standard",
                        "rate": "20.00",
                        "country": "AT"
                    },
                    {
                        "name": "Belgium Standard",
                        "rate": "21.00",
                        "country": "BE"
                    },
                    {
                        "name": "Denmark Standard",
                        "rate": "25.00",
                        "country": "DK"
                    },
                    {
                        "name": "France Standard",
                        "rate": "20.00",
                        "country": "FR"
                    },
                    {
                        "name": "Germany Standard",
                        "rate": "19.00",
                        "country": "DE"
                    }
                ]
            },
            "links": {
                "self": "https://glue.mysprykershop.com/abstract-products/001/product-tax-sets"
            }
        }
    ]
}
```
</details>

For the attributes of tax sets, see [Retrieve tax sets](/docs/pbc/all/tax-management/manage-via-glue-api/retrieve-tax-sets.html#tax-sets-response-attributes).

## Possible errors

| CODE | REASON |
|-|-|
| 301 | Abstract product is not found. |
| 311 | Abstract product SKU is not specified. |
