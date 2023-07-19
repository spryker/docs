---
title: Table Column Type Image
description: This document provides details about the Table Column Type Image in the Components Library.
template: concept-topic-template
related:
  - title: Table Column Type extension
    link: docs/marketplace/dev/front-end/page.version/table-design/table-column-types/index.html
  - title: Table Column Type Autocomplete
    link: docs/marketplace/dev/front-end/page.version/table-design/table-column-types/table-column-type-autocomplete.html
  - title: Table Column Type Chip
    link: docs/marketplace/dev/front-end/page.version/table-design/table-column-types/table-column-type-chip.html
  - title: Table Column Type Date
    link: docs/marketplace/dev/front-end/page.version/table-design/table-column-types/table-column-type-date.html
  - title: Table Column Type Dynamic
    link: docs/marketplace/dev/front-end/page.version/table-design/table-column-types/table-column-type-dynamic.html
  - title: Table Column Type Input
    link: docs/marketplace/dev/front-end/page.version/table-design/table-column-types/table-column-type-input.html
  - title: Table Column Type List
    link: docs/marketplace/dev/front-end/page.version/table-design/table-column-types/table-column-type-list.html
  - title: Table Column Type Select
    link: docs/marketplace/dev/front-end/page.version/table-design/table-column-types/table-column-type-select.html
  - title: Table Column Type Text
    link: docs/marketplace/dev/front-end/page.version/table-design/table-column-types/table-column-type-text.html
---

This document explains the Table Column Type Image in the Components library.

## Overview

Table Column Image is an Angular Component that renders an image.

Check out an example usage of the Table Column Image in the `@spryker/table` config:

```html
<spy-table
    [config]="{
        ...,
        columns: [
            ...,
            {
                id: 'columnId',
                title: 'Column Title',
                type: 'image',
                typeOptions: {
                    src: 'image URL',
                    alt: 'alt value',
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
        image: TableColumnImageConfig;
    }
}

@NgModule({
    imports: [
        TableModule.forRoot(),
        TableModule.withColumnComponents({
            image: TableColumnImageComponent,
        }),
        TableColumnImageModule,
    ],
})
export class RootModule {}
```

## Interfaces

Below you can find interfaces for the Table Column Image:

```ts
interface TableColumnImageConfig {
    src?: string;
    alt?: string;
}
```
