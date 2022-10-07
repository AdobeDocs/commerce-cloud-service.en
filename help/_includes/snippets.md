# Cloud snippets

## Elasticsearch warning {#elasticsearch-support}

>[!WARNING]
>
>Elasticsearch 7.11 and later is not supported for Adobe Commerce on cloud infrastructure. Adobe Commerce and Magento Open Source versions 2.4.4, 2.4.3-p2, and 2.3.7-p3 support the OpenSearch service. The on-premises installations continue to support Elasticsearch.

## Merge options {#merge-options}

By default, the deployment process overwrites all settings in the `env.php` file; however, you can choose to merge one or more values for a service configuration without overwriting all values.

Set the `_merge` option to one of the following:

-  `true`—**Merge** the configured service values with the environment variable values.
-  `false`—**Overwrite** the configured service values with the environment variable values.

## Private repository {#private-repository}

>[!NOTE]
>
>We strongly recommend using a private repository for your Adobe Commerce on cloud infrastructure project to protect any proprietary information or development work, such as extensions and sensitive configurations.

## Pro self-service warning {#pro-self-service-warning}

>[!WARNING]
>
>Some **Pro projects** require a support ticket to update the route configuration in the `routes.yaml` file and the cron configuration in the `.magento.app.yaml` file. Adobe recommends updating and testing YAML configuration files in an Integration environment, then deploying changes to the Staging environment. If you discover that your configuration changes are not applied to Staging sites after you redeploy and do not see any related error messages in the log, then you **MUST** submit a [Support ticket](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) that describes the attempted configuration changes. Include any updated YAML configuration files in the ticket.

## Pro services support {#pro-update-service}

>[!TIP]
>
>For Pro projects, you must submit a [Support ticket](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) to install or update services in Staging and Production environments. Indicate the service changes needed and include your updated `.magento.app.yaml` and `services.yaml` files and PHP version in the ticket. It can take up to 48 hours for the Cloud infrastructure team to update your project.

## Redeploy warning {#redeploy-warning}

>[!WARNING]
>
>Updating the environment configuration triggers a redeployment, which takes your site offline until deployment completes. Adobe recommends completing this work during off-peak hours to avoid service disruptions.

## Route placeholders {#route-placeholder}

>[!NOTE]
>
>The following route configuration examples use route templates with placeholders. The `{default}` placeholder represents the default domain configured for your site. If your project has multiple domains, use the `{all}` placeholder to configure routing for the default domain and all aliases. See [Configure routes](/help/cloud-guide/routes/routes.md.


## SCD timing {#scd-timing-warning}

>[!WARNING]
>
>If you have issues with static content files in your application after deployment, such as missing custom theme files, increase the maximum expected execution time to 900 seconds or higher.

## Scenario-based deployment {#scenarios}

>[!NOTE]
>
>With [!DNL ece-tools] 2002.1.0 and later, you can use the scenario-based deployment feature to customize the build, deploy, and post-deploy processes for your Adobe Commerce on cloud infrastructure project. See [Scenario-based deployment](https://devdocs.magento.com/cloud/deploy/scenario-based-deployment.html).

## Service instruction {#service-instruction}

Use the following instructions for service setup on Pro Integration environments and Starter environments, including the `master` branch.

>[!NOTE]
>
>You must submit a [Support ticket](https://support.magento.com/hc/en-us/articles/360000913794#support-tickets) to change the service configuration on Pro Production and Staging environments.

## Service change {#change-service-version}

>[!TIP]
>
>After initial service setup, you can change the software version for an installed service by updating the `services.yaml` and `.magento.app.yaml` configuration files. See [Change service version](/help/cloud-guide/services/services-yaml.md#change-service-version).

## Update to ece-tools {#ece-tools-package}

>[!NOTE]
>
>If you use a version of Adobe Commerce on cloud infrastructure that does not contain the `ece-tools` package, then you must perform a one-time [upgrade](/help/cloud-guide/dev-tools/install-ece-tools.md) to your cloud project to remove deprecated packages. If you currently use the `ece-tools` package and you need to update it, see [Update ece-tools version](/help/cloud-guide/dev-tools/update-ece-tools.md).

## Upgrade tip {#upgrade-tip}

>[!TIP]
>
>Before beginning an upgrade or a patching process, create an active branch from the Integration environment and check out the new branch to your local workstation. Dedicating a branch to the upgrade or the patch process helps to avoid interference with your work in progress.

## Enhanced Integration Envs {#enhanced-integration-envs}

>[!NOTE]
>
>Projects provisioned before June 5, 2020 had multiple, smaller Integration environments. If you need a larger Integration environment for testing and development, request an upgrade to Enhanced Integration environments. See the [Integration Environment request](https://support.magento.com/hc/en-us/articles/360043032152) article in the _{{site.data.var.ee}} Help Center_ for details.

## Cloud Data Collection {cloud-data-collection}

To help export Production data as test data to use in Staging and Integration environments, [Run the support utilities](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-spt-util.html):

-  [CLI commands](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-spt-util.html#config-cli-spt-utils-db) (Recommended) to export a protected backup of customer and store data using your Adobe Commerce encryption key

-  [Data Collection](https://docs.magento.com/user-guide/system/support-data-collector.html) tool for generating and exporting data

To migrate this data, see [Migrate and deploy static files and data](https://devdocs.magento.com/cloud/live/stage-prod-migrate.html).
