---
title: App Composition Platform overview
description: Learn about the App Orchestration Platform and how to use it.
template: concept-topic-template
redirect_from:
    - /docs/aop/user/intro-to-acp/acp-overview.html
---

The App Composition Platform (ACP) lets Spryker Cloud customers connect, configure, and use the available third-party services or apps, in their application with a click of a button, without development efforts from their side.

![ACP](https://spryker.s3.eu-central-1.amazonaws.com/docs/aop/app-orchestration-platform-overview/aop.png)

The following apps are supported:

- [Payone](/docs/pbc/all/payment-service-providers/payone/payone.html), a Payment Service Provider (PSP)
- [Usercentrics](/docs/pbc/all/usercentrics/usercentrics.html), a Consent Management Platform (CMP)
- [Bazaarvoice](/docs/pbc/all/ratings-reviews/{{site.version}}/third-party-integrations/bazaarvoice.html), a platform for User-Generated Content (UGC)

Spryker builds all integrations of the apps and provides them in a secure and no-code way for the SCOS.

The ACP has the following advantages:

- Quick, no-code integrations
- Fully functional trials
- Consumption-based billing
- Contains only approved and secure apps
- Always up-to-date apps

## Installing the ACP catalog

With the latest Spryker Product Release [202212.0](/docs/scos/user/intro-to-spryker/releases/release-notes/release-notes-202212.0/release-notes-202212.0.html) the ACP catalog is embedded inside the Back Office by default, but not registered with ACP yet. 

You can access the ACP catalog for now only if you are a SCOS customer and have additionally been enabled for ACP, which means that your SCOS is properly set up and registered with the ACP.

Please check [ACP installation guide](/docs/acp/user/intro-to-acp/acp-installation.html) on how to install and enable the ACP catalog for your version of SCOS.

Depending on the update status of your SCOS module versions, the type of actions and associated effort to update it to be ACP-ready may vary. The 2nd step to be ACP-enabled will always be handled by Spryker.


## Using an app from the ACP catalog

In most cases, to try an app from the ACP catalog, you do the following:

1. In the ACP catalog, select the necessary app and connect it to your shop by clicking the **Connect app** button on the app details page. You are redirected to the configuration page of the newly connected app. You can find a link to the app provider's website if you need to register with them.
2. You obtain the necessary credentials on the app provider's website.
3. In the Spryker ACP catalog, on the selected app details page, you click **Configure** and enter the credentials obtained from the app provider. Here you also make necessary settings for the app.

{% info_block infoBox "Info" %}

Make sure you check the configuration guidelines for the app you need because additional settings in the Back Office might be required for individual apps to run.

{% endinfo_block %}

That's it! You are all set to try the app out.
