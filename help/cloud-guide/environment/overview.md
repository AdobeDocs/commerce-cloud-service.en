---
title: Configuration files overview
description: Learn about configuring the cloud infrastructure environment to support deploying and managing your customized Adobe Commerce store.
feature: Cloud, Configuration, Services, Iaas, Paas
exl-id: f469a0ec-e459-413f-9725-66a0fbf34f01
---
# Configuration files overview

Environments in Adobe Commerce on cloud infrastructure include containers with applications, services, and a database to provide a complete system for your Adobe Commerce application codebase and files.

You can configure application settings, routes, build and deploy actions, and notifications to support your project environments using the following configuration files:

| Configuration | Filename | Description |
| ------------- | -------- | ----------- |
| [Application](../application/configure-app-yaml.md) | `.magento.app.yaml` | Defines how to build and deploy Adobe Commerce, including services, hooks, and cron jobs. |
| [Environment](configure-env-yaml.md) | `.magento.env.yaml` | Centralizes the management of build and deploy actions across all of your environments, including Pro Staging and Production, using environment variables. |
| [Routes](../routes/routes-yaml.md) | `.magento/routes.yaml` | Configure caching, redirects, and server-side includes. |
| [Service](../services/services-yaml.md) | `.magento/services.yaml` | Defines the services Adobe Commerce uses by name and version. For example, this file may include versions of MariaDB, PHP extensions, Redis, RabbitMQ, and Elasticsearch or OpenSearch. You must open a support ticket to push these changes to Pro plan Staging and Production environments. |
| [PHP settings](../application/php-settings.md#configure-php) | `php.ini` | An optional file that can be added to the project. The settings contained in this file are appended to the ones maintained by the cloud infrastructure. |

{style="table-layout:auto"}

## Configuration updates to Pro environments

For Adobe Commerce on cloud infrastructure Pro Staging and Production environments, you can update many configuration options in your local development environment and commit the changes to apply them to these environments. However, you must [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to update the following configuration options:

- Install or update services in the `.magento/services.yaml` file.
- Change the configuration for the `mounts` and `disk` properties in the `.magento.app.yaml` file.

{{pro-self-service-warning}}
