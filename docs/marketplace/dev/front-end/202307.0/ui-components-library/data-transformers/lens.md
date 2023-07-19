---
title: Data Transformer Lens
description: This document provides details about the Data Transformer Lens service in the Components Library.
template: concept-topic-template
related:
  - title: Data Transformers
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/index.html
  - title: Data Transformer Array-map
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/array-map.html
  - title: Data Transformer Chain
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/chain.html
  - title: Data Transformer Date-parse
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/date-parse.html
  - title: Data Transformer Date-serialize
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/date-serialize.html
  - title: Data Transformer Object-map
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/object-map.html
  - title: Data Transformer Pluck
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/pluck.html
---

This document explains the Data Transformer Lens service in the Components Library.

## Overview

Data Transformer Lens is an Angular Service that updates nested objects by path using another Data Transformer set up with a configuration object.

In the following example `datasource` will return an object with the transformed `date`.

Service configuration:

- `path`—the name of the object property, from which the value needs to be transformed. The `path` may contain nested properties separated by dots, just like in a Javascript language.  
- `transformer`—a Data Transformer that is set up with a configuration object.

```html
<spy-select
    [datasource]="{
        type: 'inline',
        data: {
            type: 'date',
            date: '2020-09-24T15:20:08+02:00',
        },
        transform: {
            type: 'lens',
            path: 'date',
            transformer: {
                type: 'date-parse',
            },
        },
    }"
>
</spy-select>
```

## Service registration

Register the service:

```ts
declare module '@spryker/data-transformer' {
    interface DataTransformerRegistry {
        lens: LensDataTransformerService;
    }
}

@NgModule({
    imports: [
        DataTransformerModule.withTransformers({
            lens: LensDataTransformerService,
        }),
    ],
})
export class RootModule {}
```

## Interfaces

Below you can find interfaces for the Data Transformer Lens:

```ts
export interface LensDataTransformerConfig extends DataTransformerConfig {
    path: string;
    transformer: DataTransformerConfig;
}
```
