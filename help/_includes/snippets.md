# Cloud snippets

## Scenario-based deployment {#scenarios}

>[!NOTE]
>
>With [!DNL ece-tools] 2002.1.0 and later, you can use the scenario-based deployment feature to customize the build, deploy, and post-deploy processes for your Adobe Commerce on cloud infrastructure project. See [Scenario-based deployment](https://devdocs.magento.com/cloud/deploy/scenario-based-deployment.html).

## Pro self-service warning {#pro-self-service-warning}

>[!WARNING]
>
>Some **Pro projects** require a support ticket to update the route configuration in the `routes.yaml` file and the cron configuration in the `.magento.app.yaml` file. Adobe recommends updating and testing YAML configuration files in an Integration environment, then deploying changes to the Staging environment. If you discover that your configuration changes are not applied to Staging sites after you redeploy and do not see any related error messages in the log, then you **MUST** submit a [Support ticket](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) that describes the attempted configuration changes. Include any updated YAML configuration files in the ticket.

## Update to ece-tools {#ece-tools-package}

>[!NOTE]
>
>If you use a version of Adobe Commerce on cloud infrastructure that does not contain the `ece-tools` package, then you must perform a one-time [upgrade](https://devdocs.magento.com/cloud/project/ece-tools-upgrade-project.html) to your cloud project to remove deprecated packages. If you currently use the `ece-tools` package and you need to update it, see [Update ece-tools version](https://devdocs.magento.com/cloud/project/ece-tools-update.html).
