---
title: Tooling config file
template: concept-topic-template
originalLink: https://documentation.spryker.com/v2/docs/tooling-config-file
originalArticleId: bb7c6781-1bdb-437b-94db-fc00df35d565
redirect_from:
  - /v2/docs/tooling-config-file
  - /v2/docs/en/tooling-config-file
related:
  - title: Code Sniffer
    link: docs/scos/dev/sdk/page.version/development-tools/code-sniffer.html
  - title: Architecture Sniffer
    link: docs/scos/dev/sdk/page.version/development-tools/architecture-sniffer.html
---

In order to make the tool configuring more convenient, we introduce the `.tooling.yml` file. It contains settings for different tools (the Architecture and the Code sniffers are supported at the moment) in one place, helping you to keep the number of files on the root level as small as possible. The `.tooling.yml` file should also be in `.gitattributes` to be ignored for tagging:

```
... export-ignore
```

## Supported tools and directives
### Code sniffer
The code sniffer configuration section can have one directive: level. Example:

```
code-sniffer:
    level: 1
 ```
 
 ### Architecture sniffer
The architecture sniffer configuration section can have two directives: priority and ignoreErrors. Example:

```
architecture-sniffer:
    priority: 5
    ignoreErrors:
        - '#DependencyProvider#'
        - '#DevelopmentCommunicationFactory#'
```

Note that the keywords listed in the **ignoreErrors** directive are regular expressions. They are used to match the lines in the error list provided as a result of the architecture sniffer doing its job.
