---
title: Back Office Translations overview
last_updated: Aug 20, 2021
description: The Back Office Translations feature introduces a way to translate the Administration interface (Zed) into different languages in a per-user manner.
template: concept-topic-template
originalLink: https://documentation.spryker.com/docs/back-office-translations-overview
originalArticleId: 3ed42aac-923f-4d04-9141-8ab480c45a18
redirect_from:
- /2021080/docs/back-office-translations-overview
- /2021080/docs/en/back-office-translations-overview
- /docs/back-office-translations-overview
- /docs/en/back-office-translations-overview

related:
  - title: Managing Users
    link: docs/scos/user/back-office-user-guides/page.version/users/roles-groups-and-users/managing-users.html
---

The _Back Office Translations_ feature introduces a way to translate the Administration interface (Zed) into different languages in a per-user manner. In terms of hierarchy, only the user with administrative rights who has access to User Control section of Zed, can manage the feature. For example, a team of developers might include a French and a German. In this case, the Shop Administrator might set up French and German Zed translations for their accounts accordingly, and those translations wouldn't interfere with each other.

There are two ways to assign a language to a user account: from the Create new User page of the User Control>User section or from the Edit User page of User Control>User section if the user is already created. Once the account language is changed, the respective user will see that their interface is translated into the corresponding language upon their next login.

Translations are added by means of uploading .csv extension files to the folders of the target modules—`data/translation/Zed/{ModuleName}/{locale_code}.csv`

File name examples can be found below:

* en_US.csv
* en_UK.csv
* de_DE.csv
* fr_FR.csv

Once a new translation file is uploaded, regenerate translation cache to reflect the changes by running the following commands:

```
translator:clean-cache
translator:generate-cache
```

Each file should consist of _key_ and _translation_ columns without headers. Example:


|  |  |
| --- | --- |
| Add Group | Gruppe hinzufügen |
| Add new Role | Neue Rolle hinzufügen |
| Add Rule | Regel hinzufügen |

{% info_block warningBox "" %}

If a translation is missing, the corresponding key is displayed instead.

{% endinfo_block %}

Unlike _Glossary_ section of Zed which is used for managing Front-end(Yves) translations, there is no interface for managing Zed translations currently. All the translations are managed by updating corresponding .csv files directly. Similarly to uploading translation files, you need to regenerate translation cache to reflect the changes after updating them. Use the commands to do that.

Newly created and all the existing modules are shipped with German translation by default. If you want to add a different language, you can follow the instructions from the [Back Office translations feature integration guide](https://documentation.spryker.com/docs/back-office-feature-integration).

The scheme below illustrates relations between Translator, UserExtension, User, UserLocale, and UserLocaleGui modules:

![image](https://spryker.s3.eu-central-1.amazonaws.com/docs/Features/Back+Office/Back+Office+Translations/Back+Office+Translations+Feature+Overview/module-diagram.png)
