---
title: Deployment process
description: Learn how deployment works for Adobe Commerce on cloud infrastructure projects.
---

# Deployment process

The deployment process begins when you perform a merge, push, or synchronization of your environment, or when you trigger a [manual redeployment](../dev-tools/cloud-cli.md#git-commands). The deployment process takes time, but there are ways to optimize deployment that depend on whether you are developing and testing or working with a live site. Most notably, you can control the [static content deployment](static-content.md).

There are three, distinct phases of the deployment process: build, deploy, and post-deploy. Each phase performs specific actions with limited resources:

## ![Build phase] Build phase

The _build_ phase assembles containers for the services defined in the configuration files, installs dependencies based on the `composer.lock` file, and runs the build hooks defined in the `.magento.app.yaml` file. Without the ability to connect to any services or access the database, the build phase depends on the resources limited to the environment.

## ![Deploy phase] Deploy phase

The _deploy_ phase places a temporary hold on incoming requests and transitions the site to [maintenance mode](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html). The deploy phase uses the new containers and, after mounting the file system, opens network connections, activates the services defined in the `relationships` section of the `.magento.app.yaml` file, and runs the deploy hooks defined in the `.magento.app.yaml` file. Everything is _read only_, except for directories defined in the `.magento.app.yaml` file. By default, the [`mounts` property](https://devdocs.magento.com/cloud/project/magento-app-properties.html#mounts) includes the following directories:

-  `app/etc`—contains the `env.php` and `config.php` configuration files
-  `pub/media`—contains all media data, such as products or categories
-  `pub/static`—contains generated static files
-  `var`—contains temporary files created during runtime

All other directories have read-only permissions. The new site becomes active at the end of the deploy phase as it transitions out of maintenance mode and releases the temporary hold on incoming requests.

## ![Post-deploy phase] Post-deploy phase

The _post-deploy_ phase runs the post-deploy hooks defined in the `.magento.app.yaml` file. Performing any action on this phase can affect site performance; however, you can use the [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) environment variable to populate the cache.

## ![Verify state] Verify configurations

You can test the optimal configuration for the state of your project by running the [Smart wizards](smart-wizards.md).

>[!NOTE]
>
>With `ece-tools` 2002.1.0 and later, you can use the scenario-based deployment feature to customize the build, deploy, and post-deploy processes for your Adobe Commerce on cloud infrastructure project. See [Scenario-based deployment](scenario-based.md).

[Build phase]: ../../assets/status-build.png
[Deploy phase]: ../../assets/status-deploy.png
[Post-deploy phase]: ../../assets/status-post-deploy.png
[Verify state]: ../../assets/status-verify.png
