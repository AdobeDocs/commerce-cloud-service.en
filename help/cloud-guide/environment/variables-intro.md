---
title: Environment variables
description: See a list of environment variables specific to Adobe Commerce on cloud infrastructure.
---

# Environment variables

Adobe Commerce on cloud infrastructure enables you to assign environment variables to override configuration options. The `ece-tools` package sets values in the `env.php` file based on values from [Cloud variables](variables-cloud.md), variables set in the Project Web interface, and the `.magento.env.yaml` configuration file.

The environment variables in the `.magento.env.yaml` file customize the Cloud environment by overriding your existing Commerce configuration. If a default value is `Not Set`, then the `ece-tools` package takes **NO** action and uses the Commerce default or the value from the `MAGENTO_CLOUD_RELATIONSHIPS` configuration. If the default value is set, then the `ece-tools` package takes the action to set that default.

The types of environment variables include:

- [ADMIN](variables-admin.md)—variables override project ADMIN variables
- [MAGENTO_CLOUD](variables-cloud.md)—variables specific to cloud infrastructure
- Variables used in the `.magento.env.yaml` file:
    - [Global](variables-global.md)—variables affect build, deploy, and post-deploy stages
    - [Build](variables-build.md)—variables control build actions
    - [Deploy](variables-deploy.md)—variables control deploy actions
    - [Post-deploy](variables-post-deploy.md)—variables control actions after deploy

Variables are _hierarchical_, which means that if a variable is not overridden, it is inherited from the parent environment.

You can set [ADMIN variables](variables-admin.md) from the Project Web interface or using the Adobe Commerce CLI. You can manage other environment variables from the [`.magento.env.yaml`](configure-env-yaml.md) file to manage build and deploy actions across all of your environments—including Pro Staging and Production—without requiring a support ticket.

>[!TIP]
>
>YAML files are case sensitive and do not allow tabs. Be careful to use consistent indentation throughout the `.magento.env.yaml` file or your configuration may not work as expected. The examples in our documentation and in the sample file use _two-space_ indentation. Use the [ece-tools validate command](configure-env-yaml.md#validate-configuration-file) to check your configuration.
