---
title: Data Transformer Collate Filter Text
description: This document provides details about the Data Transformer Collate Filter Text service in the Components Library.
template: concept-topic-template
related:
  - title: Data Transformer Filters
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/collate/filters/index.html
  - title: Data Transformer Collate Filter Equals
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/collate/filters/equals.html
  - title: Data Transformer Collate Filter Range
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/collate/filters/range.html
---

This document explains the Data Transformer Collate Filter Text service in the Components Library.

## Overview

Data Transformer Collate Filter Text is an Angular Service that implements filtering to the text value of data based on configuration.

Check out an example usage of the Data Transformer Collate Filter Text in the `@spryker/table` config:

```html
<spy-table
    [config]="{
        datasource: {
            ...,                                               
            transform: {
                ...,
                search: {
                    type: 'text',
                    propNames: ['col1', 'col2'],
                },
            },
        },
    }"
>
</spy-table>
```

## Service registration

Register the service:

```ts
declare module '@spryker/data-transformer.collate' {
    interface DataTransformerFilterRegistry {
        text: TextDataTransformerFilterService;
    }
}

@NgModule({
    imports: [
        DataTransformerModule.withTransformers({
            collate: CollateDataTransformerService,
        }),
        CollateDataTransformer.withFilters({
            text: TextDataTransformerFilterService,
        }),
    ],
})
export class RootModule {}
```

## Interfaces

Below you can find interfaces for the Data Transformer Collate Filter Text:

```ts
interface DataTransformerFilterConfig {
    type: string;
    propNames: string | string[];
}
```
