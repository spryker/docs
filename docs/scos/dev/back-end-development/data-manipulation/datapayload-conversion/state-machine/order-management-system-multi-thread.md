---
title: Order management system multi-thread
description: OMS multi-thread allows you to process OMS timeouts and conditions in parallel. Learn how to enable it.
last_updated: Jun 16, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/order-management-system-multi-thread
originalArticleId: 9472c755-7a40-4f86-b20f-1586c16385fb
redirect_from:
  - /2021080/docs/order-management-system-multi-thread
  - /2021080/docs/en/order-management-system-multi-thread
  - /docs/order-management-system-multi-thread
  - /docs/en/order-management-system-multi-thread
  - /v6/docs/order-management-system-multi-thread
  - /v6/docs/en/order-management-system-multi-thread
related:
  - title: Order process modelling via state machines
    link: docs/scos/dev/back-end-development/data-manipulation/datapayload-conversion/state-machine/order-process-modelling-via-state-machines.html
  - title: State machine console commands
    link: docs/scos/dev/back-end-development/data-manipulation/datapayload-conversion/state-machine/state-machine-console-commands.html
  - title: Common pitfalls in OMS design
    link: docs/scos/dev/back-end-development/data-manipulation/datapayload-conversion/state-machine/common-pitfalls-in-oms-design.html
  - title: Create an Order Management System - Spryker Commerce OS
    link: docs/scos/dev/back-end-development/data-manipulation/create-an-order-management-system-spryker-commerce-os.html
---

Order management system (OMS) heavily relies on the state machine-related concepts like [event timeouts](/docs/scos/dev/best-practices/state-machine-cookbook/state-machine-cookbook-state-machine-fundamentals.html#timeout) and [conditions](/docs/scos/dev/best-practices/state-machine-cookbook/state-machine-cookbook-state-machine-fundamentals.html#conditions). When an order is managed, a lot of the timeout and condition entities are being processed. Processing of timeouts and conditions in Spryker is done by two console commands:

* `oms:check-timeout`
* `oms:check-condition`

Out of the box, both of these commands process their respective entities sequentially. Each of them grabs and processes all the available entities one by one. Both commands support the `limit` option and thus can do the processing in batches. But still, all the work is done synchronously. Because of this, order management could become a bottleneck for shops with lots of orders being placed and managed. The OMS multi-thread improves this by introducing the ability to process both timeouts and conditions in parallel.

## How OMS multi-thread works
Each order is assigned a randomly generated positive number called *processor identifier*. This number is saved in `spy_sales_order` table. During the order management processing, both of the commands mentioned above are triggered with the new command option `processor-identifier` (`p`). The value of this option must match a processor identifier from `spy_sales_table`. Then the commands process only those timeouts and conditions that are related to the orders with the matching processor identifier. This way, one can, for example, trigger the `oms:check-timeout` command several times simultaneously, each time providing different processor identifiers, thus creating several PHP processes for managing a large number of orders in parallel. With the new option in place, a command looks like this:

```bash
console oms:check-timeout -p 5
```
Instead of providing a single value as the `processor-identifier` option value, one can provide several values separated by a comma.

```bash
console oms:check-timeout -p 1,2,3
```
{% info_block warningBox %}

If you have a large database, for performance reasons, it is not recommended to specify several comma-separated processor identifiers.

You need to use store name by "-s" option or limit by "-l" option to have applied "-p" option.

{% endinfo_block %}

## Enable OMS multi-thread

1. Install the `spryker/oms-multi-thread` module and update `spryker/sales`:

```bash
composer require spryker/oms-multi-thread
```

2. Apply the database changes:
```bash
console propel:install
```

3. Configure the maximum number of OMS process workers in `config/Shared/config_default.php`:

```php
...
use Spryker\Shared\OmsMultiThread\OmsMultiThreadConstants;
...

$config[OmsMultiThreadConstants::OMS_PROCESS_WORKER_NUMBER] = 10;
```

This value serves as the upper boundary for a generated processor identifier. For example, if you want to process the orders in 10 simultaneous threads, set this value to 10. Then, each new order is assigned a number between 1 and 10 as the processor identifier.

4. Configure the OMS console commands. Let's take `oms:check-timeout` as an example. Create as many cronjobs, as many process workers you have. Each cronjob must run the command with different processor identifiers within the boundaries defined in Step 3. In the current example, the maximum number of OMS process workers is 10; thus, you must configure 10 distinct cronjobs each dealing with its own processor identifier:

<details>
<summary markdown='span'>config/Zed/cronjobs/jenkins.php</summary>

```php
/* STATE MACHINE */
$jobs[] = [
    'name'     => 'check-statemachine-conditions-1',
    'command'  => '$PHP_BIN vendor/bin/console oms:check-condition -p 1',
    'schedule' => '*/10 * * * *',
    'enable'   => true,
    'run_on_non_production' => true,
    'stores'   => $allStores,
];

$jobs[] = [
    'name'     => 'check-statemachine-conditions-2',
    'command'  => '$PHP_BIN vendor/bin/console oms:check-condition -p 2',
    'schedule' => '*/10 * * * *',
    'enable'   => true,
    'run_on_non_production' => true,
    'stores'   => $allStores,
];

...

$jobs[] = [
    'name'     => 'check-statemachine-conditions-10',
    'command'  => '$PHP_BIN vendor/bin/console oms:check-condition -p 10',
    'schedule' => '*/10 * * * *',
    'enable'   => true,
    'run_on_non_production' => true,
    'stores'   => $allStores,
];
```
</details>

## General performance recommendations

Regarding performance, there are a few things to keep in mind when running the OMS commands:

* The limit options: commands `oms:check-timeout` and `oms:check-condition` have an option that allows specifying the maximum number of order items to be handled during a single command run. It's recommended to provide this option for speeding up the database-related activities.
* You can specify more than one processor identifier for a single command run. But for large databases, this is generally not recommended. Specifying more than one process identifier affects the SQL query running under the hood and might disable a table index needed for this query to be executed in the most performant way.
