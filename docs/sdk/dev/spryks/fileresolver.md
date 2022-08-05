---
title: FileResolver
description: Find out how you can enable or disable the Code Sniffer when running Spryks
template: howto-guide-template
---

The FileResolver, located in `SprykerSdk\Spryk\Model\Spryk\Builder\Resolver\FileResolverInterface`, is the core part of the file management.
It collects all the updated or created files and flushes them into the filesystem at the end of the Spryk command execution.
All the new or updated files must always be added to the FileResolver.
Normally, you shouldn't work with the file system directly by PHP functions like `file_put_contents`, `file_get_contents`, `file_exists`, and so on.
You must use `FileResolverInterface::hasResolved()`, `FileResolverInterface::resolve()`, `FileResolverInterface::addFile()`.

{% info_block warningBox "Warning" %}

Never use `resolve` or `addFile` for the core files or namespaces. You can just check these files or namespaces by `FileResolverInterface::hasResolved`.

{% endinfo_block %}