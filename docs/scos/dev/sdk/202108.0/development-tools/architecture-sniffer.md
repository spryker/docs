---
title: Architecture sniffer
description: Use Architecture Sniffer to assert a certain quality of Spryker architecture for both core and project
template: concept-topic-template
originalLink: https://documentation.spryker.com/2021080/docs/architecture-sniffer
originalArticleId: 33ab1b5b-fce7-4439-8722-87e5ecd9f3c5
redirect_from:
  - /2021080/docs/architecture-sniffer
  - /2021080/docs/en/architecture-sniffer
  - /docs/architecture-sniffer
  - /docs/en/architecture-sniffer
related:
  - title: Code Sniffer
    link: docs/scos/dev/sdk/page.version/development-tools/code-sniffer.html
---

We use our [Architecture Sniffer Tool](https://github.com/spryker/architecture-sniffer) to assert a certain quality of Spryker architecture for both core and project.

## Running the Tool
The sniffer can find a lot of violations and will report them:

```php
$ vendor/bin/console code:sniff:architecture

// Sniff a specific subfolder of your project - with verbose output
$ vendor/bin/console code:sniff:architecture src/Pyz/Zed -v

// Sniff a specific module
$ vendor/bin/console code:sniff:architecture -m Customer
```

Tip: `c:s:a` can be used as a shortcut.

Additional options:

* `-p`: Priority [1 (highest), 2 (medium), 3 (experimental)] (defaults to 2)
* `-s`: Strict (to also report those nodes with a @SuppressWarnings annotation)
* `-d`: Dry-run, only output the command to be run

Run `–help` or `-h` to get help about usage of all options available.

See the [Architecture Sniffer documentation](https://github.com/spryker/architecture-sniffer) for details and information on how to set it up for your CI system as a checking tool for each PR.

## Conventions and Guidelines
If you have a running Demoshop, go to Architecture rules in Zed backend to get an overview of all currently implemented rules.
