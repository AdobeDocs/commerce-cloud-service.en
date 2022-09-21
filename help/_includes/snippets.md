# Cloud snippets

## Elasticsearch warning {#elasticsearch-support}

>[!WARNING]
>
>Elasticsearch 7.11 and later is not supported for Adobe Commerce on cloud infrastructure. Adobe Commerce and Magento Open Source versions 2.4.4, 2.4.3-p2, and 2.3.7-p3 support the OpenSearch service. The on-premises installations continue to support Elasticsearch.

## Merge options {#merge-options}

By default, the deployment process overwrites all settings in the `env.php` file; however, you can choose to merge one or more values for a service configuration without overwriting all of the values.

Set the `_merge` option to one of the following:

-  `true`—**Merge** the configured service values with the environment variable values.
-  `false`—**Overwrite** the configured service values with the environment variable values.

## Pro self-service warning {#pro-self-service-warning}

>[!WARNING]
>
>Some **Pro projects** require a support ticket to update the route configuration in the `routes.yaml` file and the cron configuration in the `.magento.app.yaml` file. Adobe recommends updating and testing YAML configuration files in an Integration environment, then deploying changes to the Staging environment. If you discover that your configuration changes are not applied to Staging sites after you redeploy and do not see any related error messages in the log, then you **MUST** submit a [Support ticket](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) that describes the attempted configuration changes. Include any updated YAML configuration files in the ticket.

## Pro services support {#pro-update-service}

>[!TIP]
>
>For Pro projects, you must submit a [Support ticket](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) to install or update services in Staging and Production environments. Indicate the service changes needed and include your updated `.magento.app.yaml` and `services.yaml` files and PHP version in the ticket. It can take up to 48 hours for the Cloud infrastructure team to update your project.

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
>If you use a version of Adobe Commerce on cloud infrastructure that does not contain the `ece-tools` package, then you must perform a one-time [upgrade](https://devdocs.magento.com/cloud/project/ece-tools-upgrade-project.html) to your cloud project to remove deprecated packages. If you currently use the `ece-tools` package and you need to update it, see [Update ece-tools version](https://devdocs.magento.com/cloud/project/ece-tools-update.html).
