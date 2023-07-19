---
title: Data Transformer Date-serialize
description: This document provides details about the Data Transformer Date-serialize service in the Components Library.
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
  - title: Data Transformer Lens
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/lens.html
  - title: Data Transformer Object-map
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/object-map.html
  - title: Data Transformer Pluck
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/data-transformers/pluck.html
---

This document explains the Data Transformer Date-serialize service in the Components Library.

## Overview

Data Transformer Date-serialize is an Angular Service that serializes JS Date Object into a Date ISO string.

In the following example, the `datasource` transforms `date` object into the serialized `date` string.

```html
<spy-select
    [datasource]="{
        type: 'inline',
        data: Date.now(),
        transform: {
            type: 'date-serialize'
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
        'date-serialize': DateSerializeDataTransformerConfig;
    }
}

@NgModule({
    imports: [
        DataTransformerModule.withTransformers({
            'date-serialize': DateSerializeDataTransformerService,
        }),
    ],
})
export class RootModule {}
```

## Interfaces

Below you can find interfaces for the Data Transformer Date-serialize:

```ts
export interface DateSerializeDataTransformerConfig extends DataTransformerConfig {}
```
