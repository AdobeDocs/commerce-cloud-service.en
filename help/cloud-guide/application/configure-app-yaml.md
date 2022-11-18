---
title: Configure application deployment
description: Learn how to configure the properties in the application configuration file that control the way the Commerce application builds and deploys to the Cloud environment.
---

# Configure application deployment

The `.magento.app.yaml` file controls the way that your application builds and deploys. Although Adobe Commerce on cloud infrastructure supports multiple applications per project, typically, a project has a single application with the `.magento.app.yaml` file at the root of the repository.

The `.magento.app.yaml` has many default values, see [a sample `.magento.app.yaml` file](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Always review the `.magento.app.yaml` for your installed version. This file can differ across Adobe Commerce on cloud infrastructure versions.

Use the `.magento.app.yaml` file to define the following configuration values:

- [Properties](properties.md)—Define property values for application instance.
- [Variables property](variables-property.md)—Review environment variables required for the Commerce application version.
- [PHP settings](php-settings.md)—Configure runtime PHP options.
- [Set Cache For Static Files](set-cache.md)—Set cache TTL for your media and static files.
