---
title: PHP version
description: Reference information for evaluator tools.
template: howto-guide-template
redirect_from:
---

This guide describes how to resolve issues surrounding the allowed and consistent PHP version being used in different project parts.

## Problem description

The PHP version is declared in different configuration files and used by dependencies.
You need to be sure that all those items have a PHP versions that are consistent and supported by [Spryker SDK](https://docs.spryker.com/docs/sdk/dev/spryker-sdk.html).

PHP versions are checked in:
- `composer.json`
- Config deploy files `deploy.**.yml`
- [Spryker SDK](https://docs.spryker.com/docs/sdk/dev/spryker-sdk.html) PHP versions

## An example of correct code

The PHP version in your deploy files should correspond to the PHP version declared in `composer.json` and the supported PHP version by [Spryker SDK](https://docs.spryker.com/docs/sdk/dev/spryker-sdk.html).

`composer.json`:

```json
{
  "name": "spryker-shop/b2c-demo-shop",
  "description": "Spryker B2C Demo Shop",
  "license": "proprietary",
  "require": {
    "php": ">=8.0",
    ...
  }
}
```

`deploy.yml`:

```yaml
...
image:
    tag: spryker/php:8.2-alpine3.12
    php:
        ini:
            "opcache.revalidate_freq": 0
            "opcache.validate_timestamps": 0
...
```

## Example of an evaluator error message

Below is an example of an unsupported [Spryker SDK](https://docs.spryker.com/docs/sdk/dev/spryker-sdk.html) PHP version being used in the `composer.json` file:

```shell
===================
PHP VERSION CHECKER
===================

Message: Composer json PHP constraint 7.2 does not match allowed PHP versions.
Target: `{PATH_TO_PROJECT}/composer.json`
```

A `composer.json` file that produces the error message:

```json
{
  "name": "spryker-shop/b2c-demo-shop",
  "description": "Spryker B2C Demo Shop",
  "license": "proprietary",
  "require": {
    "php": "7.2",
    ...
  }
}
```

Below is an example of an unsupported [Spryker SDK](https://docs.spryker.com/docs/sdk/dev/spryker-sdk.html) PHP version being used in the `deploy.yml` file.

```shell
===================
PHP VERSION CHECKER
===================

Message: The deploy file uses a not allowed PHP image version "spryker/php:7.2-alpine3.12".
         The image tag must contain an allowed PHP version (image:abc-8.0)
Target: {PATH_TO_PROJECT}/deploy.yml
```

A `deploy.yml` file that produces the error message:

```yaml
...
image:
    tag: spryker/php:7.2
    php:
        ini:
            "opcache.revalidate_freq": 0
            "opcache.validate_timestamps": 0
...
```

Below is an example of inconsistent PHP versions being used in the `composer.json` and `deploy.yml` files:

```shell
===================
PHP VERSION CHECKER
===================

Message: Not all the targets have the same PHP versions
Target:  Current php version $phpVersion: php7.2
         tests/Acceptance/_data/InvalidProject/composer.json: -
         tests/Acceptance/_data/InvalidProject/deploy**.yml: -
         SDK php versions: php7.2, php8.2
```

The `composer.json` file uses PHP version `7.2`:

```json
{
  "name": "spryker-shop/b2c-demo-shop",
  "description": "Spryker B2C Demo Shop",
  "license": "proprietary",
  "require": {
    "php": "7.2",
    ...
  }
}
```

The `deploy.yml` file uses PHP version `8.2`:

```yaml
...
image:
    tag: spryker/php:8.2
    php:
        ini:
            "opcache.revalidate_freq": 0
            "opcache.validate_timestamps": 0
...
```

Inconsistent PHP versions produce the error message output.

## Resolve the error

To resolve the issue:
1. Use a supported [Spryker SDK](https://docs.spryker.com/docs/sdk/dev/spryker-sdk.html) PHP version.
2. Make sure that all the files contain the consistent PHP version declaration:
   - `composer.json`
   - Config deploy files `deploy.**.yml`
