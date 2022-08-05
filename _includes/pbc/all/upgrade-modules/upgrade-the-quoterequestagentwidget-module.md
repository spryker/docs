

## Upgrading from version 1.x.x to version 2.x.x

The only major change of `QuoteRequestAgentWidget` 2.x.x is the dependency update for `spryker/quote-request-agent:^2.0.0`.

*Estimated migration time: ~1h*

To migrate, do the following:

1. Update `spryker/quote-request-agent` to version ^2.0.0 by following the steps from [Migration Guide - QuoteRequestAgent](/docs/scos/dev/module-migration-guides/migration-guide-quoterequestagent.html).
2. Update `spryker-shop/quote-request-agent-widget:^2.0.0`

```bash
composer require spryker-shop/quote-request-agent-widget: "^2.0.0" --update-with-dependencies
```
