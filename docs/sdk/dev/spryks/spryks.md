---
title: Spryks
description: The Spryk code generator is a tool developed to ease the process of generating pieces of code on core and project level.
last_updated: Jun 30, 2022
template: concept-topic-template
originalLink: https://documentation.spryker.com/2021080/docs/spryk
originalArticleId: 75d7b12b-6bf1-4ace-a09d-37033947d5e5
redirect_from:
  - /2021080/docs/spryk
  - /2021080/docs/en/spryk
  - /docs/spryk
  - /docs/en/spryk
  - /v6/docs/spryk
  - /v6/docs/en/spryk
  - /v5/docs/spryk
  - /v5/docs/en/spryk
  - /v4/docs/spryk
  - /v4/docs/en/spryk
  - /v3/docs/spryk
  - /v3/docs/en/spryk
  - /v2/docs/spryk
  - /v2/docs/en/spryk
  - /docs/scos/dev/sdk/201811.0/development-tools/spryk-code-generator.html
  - /docs/scos/dev/sdk/201903.0/development-tools/spryk-code-generator.html
  - /docs/scos/dev/sdk/201907.0/development-tools/spryk-code-generator.html
  - /docs/scos/dev/sdk/202001.0/development-tools/spryk-code-generator.html
  - /docs/scos/dev/sdk/202005.0/development-tools/spryk-code-generator.html
  - /docs/scos/dev/sdk/202009.0/development-tools/spryk-code-generator.html
  - /docs/scos/dev/sdk/202108.0/development-tools/spryk-code-generator.html
  - /docs/scos/dev/sdk/development-tools/spryk-code-generator.html
---

To follow the Spryker's clean and complex architecture, you may need to write a lot of repetitive, boilerplate code. To avoid that tedious work, you can use the *Spryk* code generator, which automatically generates and modifies the required files according to the specified definitions. It also links individual code generation definitions into specific scenarios you need on a daily basis. The definitions are implemented as a set of templates with placeholders to fill out during the execution of the tool, and small pieces of code that are created or modified for each specific definition. The generated code is available for further modification by a developer.

Spryks are written with the help of YML files. The names of the YML files also represent the Spryk name. In most cases, the Spryk YML file contains arguments that are needed to run the Spryk build. Almost all Spryks need the module name to run properly, and some Spryks require much more arguments. See [Spryk configuration reference](/docs/sdk/dev/spryks/spryk-configuration-reference.html#the-root-configuration) for details on the YML file structure and arguments.

The majority of Spryks need to execute other Spryks before the called Spryk can run. For example, `Add a Zed Business Facade` needs to have a properly created module before the facade itself can be created. Therefore, Spryks have *pre* and *post* Spryks, and with the call of one Spryk, many things can and are created.

## Spryk definition types

We support the following Spryk definition types:

* **Template definitions.** A template definition adds a new file to your file system and uses Twig as a render engine, which enables you to create files from templates with placeholders. A template definition needs at least a template argument defined. The argument tells Spryk which template to use. Template definitions can have as many arguments as needed.
* **Structure definitions.** A structure definition lets you define a directory structure. For example, the `CreateSprykerModule` definition contains the description of the created directories. The main argument of a structure definition is directories, which enables you to add a list of directories to be created.
* **Method definitions.** A method definition can add methods to a specified target, such as `Spryker\Zed\FooBar\Business\FooBarFacade`. This type of definitions needs more arguments to do their job.

## Installation

To install Spryk, do the following:

1. Add this private repository to your project's `composer.json`:

```js
"repositories": [
    ...
    {
        "type": "git",
        "url": "git@github.com:spryker-sdk/spryk.git"
    }
    ...
],
```

2. Run the command:
  
```bash
composer require --dev spryker-sdk/spryk
```

## How to use Spryks

There are two interfaces to run the definitions: Spryk Console and SprykGUI.

### Spryk Console

Spryk Console is based on the Symfony's Console component. To start working with Spryk Console, add it to your `ConsoleDependencyProvider`. 
There are two commands for Spryk Console: `SprykDumpConsole` and `SprykRunConsole`. The available commands are listed in the table:

<div class="width-100">

| Command      | Description |
| ----------- | ----------- |
| vendor/bin/console spryk-dump      | Lists top level Spryks       |
| vendor/bin/spryk-dump {SPRYK NAME} | Lists of all options available for a specific Spryk |
| vendor/bin/spryk-dump --level=all | Lists all available Spryks |
| vendor/bin/console spryk-run   | Runs all Spryks in your project        |
| vendor/bin/console spryk-run {SPRYK NAME}  | Executes one specific Spryk      |
| vendor/bin/spryk-build | Reflects changes in Spryk arguments and generates a new cache for them |

</div>

When you run a Spryk, the console asks you to provide all the needed arguments to build the Spryk. It is also possible to print all possible arguments to the console by using the `--{argument name}={argument value}` key.

### SprykGUI

This is a Graphical User Interface built inside the Back Office application. To install it, run this command:

```bash
composer require --dev spryker-sdk/spryk-gui
```

Once SprykGUI is installed, you can navigate to it through the Back Office. There you can find the list of all the available definitions, and after you have clicked on one of them, the form where you can enter the arguments appears.

## Core and Project modes

The difference between the Core and Project modes is the place where your code is generated.

- *Core* has the `vendor/spryker/{% raw %}{{{% endraw %} organization {% raw %}}}{% endraw %}/ root` path;
- *Project* has the `src/{% raw %}{{{% endraw %} organization {% raw %}}}{% endraw %}/ root` path.

You should put the organization option into the namespaces config files (Core or Project).

{% info_block warningBox "Warning" %}

Not all Spryk definitions can be run on Project layers.

{% endinfo_block %}

### How to change the mode

By default, all Spryk definitions run in the *Project* mode. To use the *Core* mode, run
the command

```bash
console spryk:run {% raw %}{{{% endraw %} SprykName {% raw %}}}{% endraw %}
```
with the `--mode='core'` argument in CLI.
This being done, Spryk will use the *Core* mode and an appropriate root path.

## Creating a definition

As the whole tool is covered by tests, you should also start to create your own definition by adding a test. To add only a new definition configuration, start by adding an integration test. You also need to add the name of the definition you want to test (for example, *AddMySuperNiceFile*), and the assertion to have this file created after you have executed the test.

Once done, run the integration tests with the following command and see the test fail:

```bash
vendor/bin/codecept run Integration -g {YOUR TEST GROUP}
```

This shows a message that the definition was not found by the given name. Therefore, add the definition file for your new definition to `spryker/spryk/config/spryk/spryks`. After that, re-run the tests.

What comes next depends on the chosen definition type. If you have selected the template definition, then most likely you will see an error indicating that the defined template cannot be found. In this case, add your template to `spryker/spryker/config/spryk/templates` and re-run the tests—now they should be green.

## Extending Spryks

There are two ways to extend the Spryks: by adding new Spryks and by adding the Spyrk templates.

### Adding Spryks

You can add your own Spryks by creating a Spryk definition in your project's `config/spryk/spryks/` directory. The tool will find the Spryk definitions in this directory, and the Spryk definitions can be executed as usual.

For more information on adding new Spryks, see [Adding a new Spryk](/docs/sdk/dev/spryks/adding-a-new-spryk.html).

### Adding Spryk templates

To add s Spryk template, create the template in your project's `config/spryk/templates/` directory.

The tool will find the Spryk templates in this directory, and the template can be used in your Spryks.

## Configuration

Spryks need some project-related configurations. These are passed automatically to the tool.

The following configurations are passed to the Spryk tool:

- `Spryker\Shared\Kernel\KernelConstants::PROJECT_NAMESPACE`
- `Spryker\Shared\Kernel\KernelConstants::PROJECT_NAMESPACES`
- `Spryker\Shared\Kernel\KernelConstants::CORE_NAMESPACES`