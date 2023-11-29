---
title: Data Exchange
description: General information about the data exchange options.
template: concept-topic-template
---

Data Exchange refers to the process of transferring data between Spryker and third-party systems.

Spryker offers the following options to import and export data:

- Spryker Middleware powered by Alumio:
    - Spryker Integration Apps
    - Custom integrations using the existing Alumio connectors
    - Custom integration apps using the Alumio SDK to build your own connectors
- Data Exchange API: available in SCCOS by default
- Data Importers and Data Exporters: available in Spryker Cloud Commerce OS (SCCOS) by default


## Spryker Middleware powered by Alumio

{% include pbc/all/data-exchange/202311.0/spryker-middleware-powered-by-alumio.md %} <!-- To edit, see /_includes/pbc/all/data-exchange/202311.0/spryker-middleware-powered-by-alumio.md -->

### Spryker Integration Apps

{% include pbc/all/data-exchange/202311.0/spryker-integration-apps.md %} <!-- To edit, see /_includes/pbc/all/data-exchange/202311.0/spryker-integration-apps.md -->

### Custom integrations with Alumio connectors

{% include pbc/all/data-exchange/202311.0/custom-integrations-with-alumio-connectors.md %} <!-- To edit, see /_includes/pbc/all/data-exchange/202311.0/custom-integrations-with-alumio-connectors.md -->

### Custom integrations with custom connectors

{% include pbc/all/data-exchange/202311.0/custom-integrations-with-custom-connectors.md %} <!-- To edit, see /_includes/pbc/all/data-exchange/202311.0/custom-integrations-with-custom-connectors.md -->

## Data Exchange API

Data Exchange API is a dynamic database API that facilitates data transfer in real-time, ensuring data is always current across all integrated platforms. It's part of the SCCOS platform core.

Data Exchange API lets you build, customize, and manage APIs tailored to your specific business requirements through a user interface.

The main benefits of the Data Exchange API include the following:

- No coding is required: The API endpoints are created from the user interface.
- Rapid API generation: The APIs are generated within minutes.
- Flexibility and customization: You can tailor APIs to your needs. You can define parameters to ensure compatibility with your systems.
- Real-time updates: The infrastructure supports dynamic changes, so you can modify APIs on the fly.
- Security and Access Control: The infrastructure incorporates strong security measures and access controls, which safeguards sensitive information.

We recommend considering the Data Exchange API in the following cases:

- You want to implement a data integration via API with a middleware that's not [Alumio](https://www.alumio.com).
- You want to create your own data integration engine via API, without using any middleware software.


## Data Importers and Data Exporters

Data Importers and Data Exporters are tools that let you bring external data into and send data from SCCOS, using .CSV files.  Data Importers and Data Exporters are part of the SCCOS platform core.
Data Importers and Data Exporters require extensive customization development for each project and ongoing development effort, which makes them less suitable for demanding data exchange.

For information on how Data importers and Exporters work, see [Data import](/docs/scos/dev/data-import/{{site.version}}/data-import.html) and [Data export](/docs/pbc/all/order-management-system/{{page.version}}/base-shop/import-and-export-data/orders-data-export/orders-data-export.html).
