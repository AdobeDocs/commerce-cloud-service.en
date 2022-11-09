---
title: "[!DNL Ece-tools] Package"
description: Learn about the [!DNL Ece-tools] package and how it helps to manage and deploy Adobe Commerce.
---

# ECE-Tools Package

The [!DNL ece-tools] package is a set of scripts and tools designed to manage and deploy the Commerce application. The [!DNL ece-tools] package simplifies many processes, such as managing cron jobs, verifying project configuration, and applying Adobe patches and hot fixes. You can view and contribute to the [open-source [!DNL ece-tools] code repository on GitHub][ece-repo].

{{ece-tools-package}}

The `ece-tools` package is compatible with Adobe Commerce—starting with version 2.1.4—and contains scripts and Adobe Commerce on cloud infrastructure commands designed to help manage your code and automatically build and deploy your projects.

The following lists the available `ece-tools` commands:

```bash
php ./vendor/bin/ece-tools list
```

## Build and deploy

The `ece-tools` package contains commands to perform operations for the build, deploy, and post-deploy stages of launching your Adobe Commerce on cloud infrastructure application. For example, the `php ./vendor/bin/ece-tools build` command begins the application build process.

By default, these `ece-tools` commands are in the [hooks property](../application/hooks-property.md) of the `.magento.app.yaml` configuration file.

## Docker configuration generator

The `ece-tools` package includes a dependency for the [magento/magento-cloud-docker][] package, which provides functionality and configuration files for Docker images to launch a Docker development environment for Adobe Commerce on cloud infrastructure. You can also run Cloud Docker for Commerce as a stand-alone package. See [Docker development][docker].

## Services, routes, and variables

You can use the `ece-tools` package to display detailed information about the Base64-encoded [Cloud variables](../environment/variables-cloud.md) used in any Cloud environment. The following command shows all services, routes, and variables.

```bash
php ./vendor/bin/ece-tools env:config:show
```

To display a specific set of information, use the following format:

```bash
php ./vendor/bin/ece-tools env:config:show <option>
```

-  `services`—Displays the relationship data from the `MAGENTO_CLOUD_RELATIONSHIPS` environment variable, defined in the `services.yaml` file.
-  `routes`—Displays the configured routes for the project using the `MAGENTO_CLOUD_ROUTES` environment variable.
-  `variables`—Displays the configured variables for the project using the `MAGENTO_CLOUD_VARIABLES` environment variable.

Sample output for the `services` option:

```terminal
Magento Cloud Services:
+-----------------------------------+----------------------------------+
| Service Configuration             | Value                            |
+-----------------------------------+----------------------------------+
| database:                                                            |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| password                          | <password>                       |
| port                              | 3306                             |
+-----------------------------------+----------------------------------+
| elasticsearch:                                                       |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| port                              | 9200                             |
...
```

## Verify environment configuration

There is a set of verification commands available to help evaluate the configuration of your project. See [Smart wizards](../deploy/smart-wizards.md) in the _Optimize deployment_ section for a detailed description of each wizard command. The `wizard:ideal-state` command runs automatically during the build phase. To verify the ideal state of your project:

```bash
php ./vendor/bin/ece-tools wizard:ideal-state
```

>[!NOTE]
>
>You must run the `wizard:ideal-state` command in the remote Cloud environment. The command always returns the `The configured state is not ideal` error when run in the local development environment.

Sample output:

```terminal
Ideal state is configured
```

See [Release notes for ece-tools](../release-notes/cloud-tools.md).

## Adobe patches and custom patches

The `ece-tools` package includes a dependency for the [magento/magento-cloud-patches][] package, which delivers Adobe patches and hot fixes that improve the integration of all Adobe Commerce versions with Cloud environments and supports quick delivery of critical fixes. The `` also delivers custom patches that you add to your Adobe Commerce on cloud infrastructure project. See [Apply patches](../development/apply-patches.md).

<!-- link definitions -->

[docker]: https://devdocs.magento.com/cloud/docker/docker-development.html
[ece-repo]: https://github.com/magento/ece-tools
[magento/magento-cloud-docker]: https://github.com/magento/magento-cloud-docker
[magento/magento-cloud-patches]: https://github.com/magento/magento-cloud-patches
