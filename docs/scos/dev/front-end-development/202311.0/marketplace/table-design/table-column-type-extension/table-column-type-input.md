---
title: Table Column Type Input
description: This document provides details about the Table Column Type Input in the Components Library.
template: concept-topic-template
redirect_from:
  - /docs/marketplace/dev/front-end/202212.0/table-design/table-column-types/table-column-type-input.html
related:
  - title: Table Column Type extension
    link: docs/scos/dev/front-end-development/page.version/marketplace/table-design/table-column-type-extension/table-column-type-extension.html
  - title: Table Column Type Autocomplete
    link: docs/scos/dev/front-end-development/page.version/marketplace/table-design/table-column-type-extension/table-column-type-autocomplete.html
  - title: Table Column Type Chip
    link: docs/scos/dev/front-end-development/page.version/marketplace/table-design/table-column-type-extension/table-column-type-chip.html
  - title: Table Column Type Date
    link: docs/scos/dev/front-end-development/page.version/marketplace/table-design/table-column-type-extension/table-column-type-date.html
  - title: Table Column Type Dynamic
    link: docs/scos/dev/front-end-development/page.version/marketplace/table-design/table-column-type-extension/table-column-type-dynamic.html
  - title: Table Column Type Image
    link: docs/scos/dev/front-end-development/page.version/marketplace/table-design/table-column-type-extension/table-column-type-image.html
  - title: Table Column Type List
    link: docs/scos/dev/front-end-development/page.version/marketplace/table-design/table-column-type-extension/table-column-type-list.html
  - title: Table Column Type Select
    link: docs/scos/dev/front-end-development/page.version/marketplace/table-design/table-column-type-extension/table-column-type-select.html
  - title: Table Column Type Text
    link: docs/scos/dev/front-end-development/page.version/marketplace/table-design/table-column-type-extension/table-column-type-text.html
---

This document explains the Table Column Type Input in the Components library.

## Overview

Table Column Input is an Angular Component that renders a field using the `@spryker/input` component.

Check out an example usage of the Table Column Input in the `@spryker/table` config:

```html
<spy-table
    [config]="{
        ...,
        columns: [
            ...,
            {
                id: 'columnId',
                title: 'Column Title',
                type: 'input',
                typeOptions: {
                    type: 'number',
                    attrs: {
                        step: 0.05,
                    },
                },
            },
            ...,
        ],
    }"
>
</spy-table>
```

## Component registration

Register the component:

```ts
declare module '@spryker/table' {
    interface TableColumnTypeRegistry {
        input: TableColumnInputConfig;
    }
}

@NgModule({
    imports: [
        TableModule.forRoot(),
        TableModule.withColumnComponents({
            input: TableColumnInputComponent,
        }),
        TableColumnInputModule,
    ],
})
export class RootModule {}
```

## Interfaces

Below you can find interfaces for the Table Column Input:

```ts
interface TableColumnInputConfig {
    /** Bound to the @spryker/input inputs */
    type: string; // 'text' - by default
    value?: any;
    placeholder: string;
    prefix?: string;
    suffix?: string;
    outerPrefix?: string;
    outerSuffix?: string;
    attrs?: Record<string, string>;
    /** Bound to the @spryker/form-item input */
    editableError?: string | boolean;
}
```
