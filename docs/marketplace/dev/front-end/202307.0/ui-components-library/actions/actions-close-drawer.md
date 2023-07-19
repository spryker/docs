---
title: Actions Close Drawer
description: This document provides details about the Actions Close Drawer service in the Components Library.
template: concept-topic-template
related:
  - title: Actions
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/index.html
  - title: Actions Drawer
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-drawer.html
  - title: Actions HTTP
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-http.html
  - title: Actions Notification
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-notification.html
  - title: Actions Redirect
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-redirect.html
  - title: Actions Refresh Drawer
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-refresh-drawer.html
  - title: Actions Refresh Parent Table
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-refresh-parent-table.html
  - title: Actions Refresh Table
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-refresh-table.html

---

This document explains the Actions Close Drawer service in the Components Library.

## Overview

Actions Close Drawer is an Angular Service that closes the first Drawer in the current context.

Check out an example usage of the Actions Close Drawer.

Service configuration:

- `type`—an action type.

```html
<spy-button-action
    [action]="{
        type: 'close-drawer',
    }"
>
</spy-button-action>
```

## Service registration

Register the service:

```ts
declare module '@spryker/actions' {
    interface ActionsRegistry {
        'close-drawer': CloseDrawerActionHandlerService;
    }
}

@NgModule({
    imports: [
        ActionsModule.withActions({
            'close-drawer': CloseDrawerActionHandlerService,
        }),
    ],
})
export class RootModule {}
```

## Interfaces

Below you can find interfaces for the Actions Close Drawer:

```ts
export interface CloseDrawerActionConfig extends ActionConfig {}
```
