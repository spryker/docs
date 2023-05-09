---
title: Connect Spryker Code Upgrader to a Azure managed project
description: Learn how to connect Spryker Code Upgrader to a Azure managed project
template: howto-guide-template
redirect_from:
  - /docs/paas-plus/dev/onboard-to-spryker-code-upgrader/connect-spryker-code-upgrader-to-a-azure-managed-project.html
---

## Connect Spryker Code Upgrader using Azure access token

To connect the Upgrader manually using a Azure access token, follow the steps.

## Prerequisites

1. Generate Git credentials.

Open **Clone Repository** window in your Azure repository and click on **Generate Git credentials** button.

![Generate Git credentials](https://spryker.s3.eu-central-1.amazonaws.com/docs/paas%2B/dev/onboard-to-spryker-code-upgrader/connect-spryker-code-upgrader-to-a-azure-managed-project.md/generate_git_credentials.png)

2. [Create a Azure access token](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate#create-a-pat)

Azure access token should have the following repository permissions:

* **Code (Read & write)** for Spryker Upgrader Service: grants read and write access to the repository to enable the Upgrader to analyze the project and create PRs.

## Configure the connection in Spryker CI

1. In Spryker CI, go to **Projects**.
2. On the **Projects** page, select the **Spryker Upgrade Service** project.

![Spryker CI Projects](https://spryker.s3.eu-central-1.amazonaws.com/docs/paas%2B/dev/onboard-to-spryker-code-upgrader/connect-spryker-code-upgrader-to-a-azure-managed-project.md/spryker_ci_projects.png)

3. Go to **Code**.

![Spryker CI Code](https://spryker.s3.eu-central-1.amazonaws.com/docs/paas%2B/dev/onboard-to-spryker-code-upgrader/connect-spryker-code-upgrader-to-a-azure-managed-project.md/spryker_ci_code_page.png)

4. In the **Connect Git repository** pane, for **GIT HOSTING PROVIDER**, select **Private Server**.

5. For **AUTHENTICATION METHOD** select **Password**.

![Spryker CI Code Azure](https://spryker.s3.eu-central-1.amazonaws.com/docs/paas%2B/dev/onboard-to-spryker-code-upgrader/connect-spryker-code-upgrader-to-a-azure-managed-project.md/azure_code_add.png)

6. Enter your Azure repository URL, username and password, and click on **Connect repository** button.

{% info_block infoBox "Repository URL" %}

Repository URL should be in format `https://dev.azure.com/<organization_name>/<project_name>/_git/<repository_name>` (without the `<organization_name>@` prefix).

{% endinfo_block %}

## Support for Spryker CI

* For help with Spryker CI, [contact support](https://spryker.force.com/support/s/).
* To learn more about Buddy, see their [docs](https://buddy.works/docs).

## Next steps

[Run Spryker Code Upgrader](/docs/scu/dev/run-spryker-code-upgrader.html)
