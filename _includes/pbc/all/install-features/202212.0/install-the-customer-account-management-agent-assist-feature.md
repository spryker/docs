

This document describes how to integrate the Customer Account Management + Agent Assist feature into a Spryker project.

## Install feature core

Follow the steps below to install the Customer Account Management + Agent Assist feature core.

### Prerequisites

To start the feature integration, overview and install the necessary features:

| NAME                        | VERSION          | INTEGRATION GUIDE                                                                                                                                                  |
|-----------------------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Customer Account ManagemenT | {{site.version}} | [Customer Account Management feature integration](/docs/scos/dev/feature-integration-guides/{{site.version}}/customer-account-management-feature-integration.html) |
| Agent Assist                | {{site.version}} | [Install the Agent Assist feature](/docs/pbc/all/user-management/{{site.version}}/install-and-upgrade/install-the-agent-assist-feature.html)                               |

### 1) Install the required modules using composer

```bash
composer require spryker/oauth-agent-connector:"^1.0.0" --update-with-dependencies
```

{% info_block warningBox "Verification" %}

Ensure that the following module has been installed:

| MODULE              | EXPECTED DIRECTORY                   |
|---------------------|--------------------------------------|
| OauthAgentConnector | vendor/spryker/oauth-agent-connector |

{% endinfo_block %}

### 2) Set up configuration

Activate the following plugin:

| PLUGIN                         | SPECIFICATION                         | PREREQUISITES | NAMESPACE                                                      |
|--------------------------------|---------------------------------------|---------------|----------------------------------------------------------------|
| AgentOauthScopeInstallerPlugin | Installs agent-specific OAuth scopes. | None          | Spryker\Zed\OauthAgentConnector\Communication\Plugin\Installer |


**src/Pyz/Zed/Installer/InstallerDependencyProvider.php**

```php
<?php

namespace Pyz\Zed\Installer;

use Spryker\Zed\Installer\InstallerDependencyProvider as SprykerInstallerDependencyProvider;
use Spryker\Zed\OauthAgentConnector\Communication\Plugin\Installer\AgentOauthScopeInstallerPlugin;

class InstallerDependencyProvider extends SprykerInstallerDependencyProvider
{
    /**
     * @return \Spryker\Zed\Installer\Dependency\Plugin\InstallerPluginInterface[]
     */
    public function getInstallerPlugins()
    {
        return [
            new AgentOauthScopeInstallerPlugin(),
        ];
    }
}
```

{% info_block warningBox "Verification" %}

Ensure that `console setup:init-db` installs agent-specific scopes configured in `OauthAgentConnectorConfig::getAgentScopes()`.

{% endinfo_block %}

### 3) Set up transfer objects

Generate transfer changes:

```bash
console transfer:generate
```

{% info_block warningBox "Verification" %}

Ensure that the following changes have been applied in the transfer objects:

| TRANSFER                            | TYPE     | EVENT   | PATH                                                              |
|-------------------------------------|----------|---------|-------------------------------------------------------------------|
| CustomerIdentifierTransfer.idAgent  | property | created | src/Generated/Shared/Transfer/CustomerIdentifierTransfer          |
| OauthScopeTransfer                  | class    | created | src/Generated/Shared/Transfer/OauthScopeTransfer                  |
| OauthUserTransfer                   | class    | created | src/Generated/Shared/Transfer/OauthUserTransfer                   |
| OauthClientTransfer                 | class    | created | src/Generated/Shared/Transfer/OauthClientTransfer                 |
| OauthScopeRequestTransfer           | class    | created | src/Generated/Shared/Transfer/OauthScopeRequestTransfer           |
| FindAgentResponseTransfer           | class    | created | src/Generated/Shared/Transfer/FindAgentResponseTransfer           |
| OauthGrantTypeConfigurationTransfer | class    | created | src/Generated/Shared/Transfer/OauthGrantTypeConfigurationTransfer |
| UserTransfer                        | class    | created | src/Generated/Shared/Transfer/UserTransfer                        |

{% endinfo_block %}

### 4) Set up behavior

Activate the following plugins:

| PLUGIN                                                      | SPECIFICATION                                                                           | PREREQUISITES | NAMESPACE                                                    |
|-------------------------------------------------------------|-----------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------|
| AgentOauthUserProviderPlugin                                | Authenticates an Agent, reads Agent data and provides it for the access token.          | None          | Spryker\Zed\OauthAgentConnector\Communication\Plugin\Oauth   |
| AgentOauthScopeProviderPlugin                               | Provides the Agent scopes.                                                              | None          | Spryker\Zed\OauthAgentConnector\Communication\Plugin\Oauth   |
| AgentCredentialsOauthGrantTypeConfigurationProviderPlugin   | Provides configuration of the`agent_credentials` grant type.                            | None          | Spryker\Zed\OauthAgentConnector\Communication\Plugin\Oauth   |
| UpdateAgentSessionAfterCustomerAuthenticationSuccessPlugin  | Updates agent's session data in storage if access is granted and an agent is logged in. | None          | SprykerShop\Yves\SessionAgentValidation\Plugin\CustomerPage  |

<details open><summary markdown='span'>src/Pyz/Zed/Oauth/OauthDependencyProvider.php</summary>

```php
<?php

namespace Pyz\Zed\Oauth;

use Spryker\Zed\Oauth\OauthDependencyProvider as SprykerOauthDependencyProvider;
use Spryker\Zed\OauthAgentConnector\Communication\Plugin\Oauth\AgentCredentialsOauthGrantTypeConfigurationProviderPlugin;
use Spryker\Zed\OauthAgentConnector\Communication\Plugin\Oauth\AgentOauthScopeProviderPlugin;
use Spryker\Zed\OauthAgentConnector\Communication\Plugin\Oauth\AgentOauthUserProviderPlugin;

class OauthDependencyProvider extends SprykerOauthDependencyProvider
{
    /**
     * @return \Spryker\Zed\OauthExtension\Dependency\Plugin\OauthUserProviderPluginInterface[]
     */
    protected function getUserProviderPlugins(): array
    {
        return [
            new AgentOauthUserProviderPlugin(),
        ];
    }

    /**
     * @return \Spryker\Zed\OauthExtension\Dependency\Plugin\OauthScopeProviderPluginInterface[]
     */
    protected function getScopeProviderPlugins(): array
    {
        return [
            new AgentOauthScopeProviderPlugin(),
        ];
    }

    /**
     * @return \Spryker\Zed\OauthExtension\Dependency\Plugin\OauthGrantTypeConfigurationProviderPluginInterface[]
     */
    protected function getGrantTypeConfigurationProviderPlugins(): array
    {
        return array_merge(parent::getGrantTypeConfigurationProviderPlugins(), [
            new AgentCredentialsOauthGrantTypeConfigurationProviderPlugin(),
        ]);
    }
}
```

</details>

**src/Pyz/Yves/CustomerPage/CustomerPageDependencyProvider.php**

```php
<?php

namespace Pyz\Yves\CustomerPage;

use SprykerShop\Yves\CustomerPage\CustomerPageDependencyProvider as SprykerShopCustomerPageDependencyProvider;
use SprykerShop\Yves\SessionAgentValidation\Plugin\CustomerPage\UpdateAgentSessionAfterCustomerAuthenticationSuccessPlugin;

class CustomerPageDependencyProvider extends SprykerShopCustomerPageDependencyProvider
{
    /**
     * @return array<\SprykerShop\Yves\CustomerPageExtension\Dependency\Plugin\AfterCustomerAuthenticationSuccessPluginInterface>
     */
    protected function getAfterCustomerAuthenticationSuccessPlugins(): array
    {
        return [
            new UpdateAgentSessionAfterCustomerAuthenticationSuccessPlugin(),
        ];
    }
}
```

{% info_block warningBox "Verification" %}

Ensure that the Agent can get the access token with valid credentials by sending the request:

**Request sample**

`POST https://glue.mysprykershop.com/agent-access-tokens`

```json
{
    "data": {
        "type": "agent-access-tokens",
        "attributes": {
            "username": "admin@spryker.com",
            "password": "change123"
        }
    }
}
```

**Expected response**

```json
{
    "data": {
        "type": "agent-access-tokens",
        "id": null,
        "attributes": {
            "tokenType": "Bearer",
            "expiresIn": 28800,
            "accessToken": "eyJ0eXAiOiJKV1QiLCJhbGciOi...",
            "refreshToken": "def50200d0f922e0c1e981add4..."
        },
        "links": {
            "self": "https://glue.mysprykershop.com/agent-access-tokens"
        }
    }
}
```


{% endinfo_block %}

## Related features

Install the following related features:

| FEATURE                     | INTEGRATION GUIDE                                                                                                                                                 |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Customer Account Management | [Customer Acount Management feature integration](/docs/scos/dev/feature-integration-guides/{{site.version}}/customer-account-management-feature-integration.html) |
| Agent Assist                | [Install the Agent Assist feature](/docs/pbc/all/user-management/{{site.version}}/install-and-upgrade/install-the-agent-assist-feature.html)                              |
| Agent Assist API            | [Glue API: Agent Assist feature integration](/docs/pbc/all/user-management/{{site.version}}/install-and-upgrade/install-the-agent-assist-glue-api.html)  |
