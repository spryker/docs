---
title: "Oryx: Providing component definitions"
description: Components are registered in an Oryx application by a definition file
last_updated: Sept 19, 2023
template: concept-topic-template
---

Oryx components can be used in different ways. They can be configured in [pages](/docs/scos/dev/front-end-development/{{page.version}}/oryx/building-pages/oryx-pages.html) and [compositions](/docs/scos/dev/front-end-development/{{page.version}}/oryx/building-pages/oryx-compositions.html), used in components, or integrated in CMS content.

When a component is rendered for the first time, Oryx resolves the component definition from the registry and loads the associated implementation. With this, components are lazily loaded.

To register a [component implementation](/docs/scos/dev/front-end-development/{{page.version}}/oryx/building-components/oryx-implementing-components.html), you need to provide a component definition. The component definition requires a name and an implementation. The name is used as the web component element name and consists of two or more words separated by a dash. We recommend prefixing component names with a project, brand, or company name. For example, Oryx components are prefixed with `oryx-`.

{% info_block infoBox "Update definitions" %}
You can also update an existing component definition. To match an existing definition, you still need to provide a name.
{% endinfo_block %}

The following example shows where a component is registered, providing both the name and implementation.

```ts
import { componentDef } from "@spryker-oryx/utilities";

export const productIdComponent = componentDef({
  name: "oryx-product-id",
  impl: () => import("./id.component").then((m) => m.ProductIdComponent),
});
```

The [dynamic `import()` expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import) is used to ensure the component is lazily loaded. Dynamic imports are used by build systems like [Vite](https://vitejs.dev/) to create a separate JavaScript chunk during the build. This allows to load the JavaScript chunk upon demand.

Lazy loading components is the recommended technique as it avoids loading all the application components at startup of the application. Components are only loaded when they are used, which increases the application's performance.

{% info_block warningBox "Static import of component files" %}

To prevent breaking the lazy loading principals, do not import component files _statically_.

{% endinfo_block %}
