---
title: New Relic log management
description: Learn how to use the New Relic log
feature: Cloud, Logs, Observability
---

# New Relic log management

All cloud infrastructure projects include [New Relic log management](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/). The service is pre-configured to aggregate all log data from your Staging and Production environments and display it in a centralized log management dashboard.

The aggregated data includes information from the following logs:

- All `ece-tools` and application logs from the `~/var/log` directory
- Logs for cloud services from the `var/log/platform/<project-ID>` directory
- Fastly CDN and WAF

When your project is connected to New Relic, you can use the New Relic Logs service to complete tasks like the following:

- Use [New Relic queries] to search aggregated log data
- Visualize log data through the New Relic Logs application
- Create custom charts, dashboards, and alerts
- Troubleshoot performance issues from a single dashboard

## View and analyze log data

You can use the New Relic Logs application to search across the aggregated log data and troubleshoot application, infrastructure, CDN, and WAF errors. Also, you can connect the log data with other data collected by New Relic APM and Infrastructure services to create charts, dashboards, and alerts to manage application and cloud service operations.

**To use the New Relic Logs application**:

1. Log in to your [New Relic account](https://login.newrelic.com/login).

1. Select **Logs** from the Explorer navigation menu.

1. Verify you have the correct Account selected at the top of the _All logs_ view.

1. To review infrastructure log data for cloud services, enter the query string `has: "filePath"` in the _Find logs where_ field. Then, click **Query logs**.

   The names of the log files are stored in the `filePath` field, with full paths to the log file.

   ![Cloud project New Relic service log data](../../assets/new-relic/log-query.png)

1. To review Fastly log data, enter the query string `has: "client_ip"` in the _Find logs where_ field. Then, click **Query logs**.

1. To filter the Fastly log results further, select an attribute from the left menu, then click **Query logs** to apply the updated query.

   For example, to query the Fastly data by country code, select the _Geo Country Code_ attribute.

   ![Cloud project New Relic CDN log attribute filter](../../assets/new-relic/fastly-countrycode-filter.png)

See [Get started with log management](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/) and [Introduction to the New Relic query language](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/introduction-nrql-new-relics-query-language/) on the _New Relic Docs_ site.
