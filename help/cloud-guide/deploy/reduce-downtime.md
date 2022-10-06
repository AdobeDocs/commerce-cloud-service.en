---
title: Zero downtime deployment
description: Learn how to reduce overall downtime when deploying Adobe Commerce on cloud infrastructure projects.
---

# Zero downtime deployment

Adobe Commerce on cloud infrastructure runs the application in [_maintenance_ mode](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html#production-mode) during the deploy phase, which takes your site offline until the deployment is complete. The length of time your Production site is in maintenance mode depends on the size of the site, the number of changes applied during the deployment, and the configuration for static content deployment. It is possible to configure your project so that it deploys with a **zero** downtime effect.

During the deployment process, all connections queue for up to 5 minutes preserving any active sessions and pending actions, such as adding to cart or checkout. After deployment, the queue is released and connections continue without interruption. To use this _connection hold_ to your advantage and reduce deployment to _zero_ downtime, you must configure your project to use the most efficient deploy strategy.

Use the following steps to reduce the amount of time it takes your store to deploy an update to Production:

1. [Upgrade to the `ece-tools` package](https://devdocs.magento.com/cloud/project/ece-tools-upgrade-project.html) or [update the `ece-tools` version](https://devdocs.magento.com/cloud/project/ece-tools-update.html)
   Your Adobe Commerce on cloud infrastructure project must have the latest `ece-tools` package so that you have the tools available to configure an optimal deployment. If you have the latest `ece-tools`, continue to the next step.

   >[!NOTE]
   >
   >Even though it is a best practice to use the latest `ece-tools` package, the zero-downtime deployment method works with `ece-tools` [version 2002.0.13](https://devdocs.magento.com/cloud/release-notes/cloud-release-archive.html#v2002013) and later.

1. [Configure static content deployment](static-content.md)
   If static content deployment fails in the deploy phase, your site gets stuck in maintenance mode. When a failure occurs during the build phase, the process avoids downtime because it never begins the deploy phase. [Generating static content during the build phase with minified HTML](static-content.md#setting-the-scd-on-build), also known as the ideal state, is the optimal configuration for zero-downtime deployments and _prevents_ downtime if a failure occurs.

1. [Configure the post-deploy hook](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks)
   You must configure the post-deploy hook to clean and warm the cache. By default, cache clean occurs during the deploy phase when the site is down. Moving the cache clean to the post-deploy phase means that your cache remains live until the deploy phase is complete, and then you can safely clean the cache.

   Customize the list of pages used to preload the cache with the [WARM_UP_PAGES environment variable](../environment/variables-post-deploy.md#warmuppages).

1. [Reduce theme files](../environment/variables-deploy.md#scdmatrix)
   You can reduce the number of unnecessary theme files by configuring the SCD\_MATRIX environment variable.

1. [Speed up static content deployment](../environment/variables-deploy.md#scdthreads)
   You can speed up the deployment process by updating the  SCD\_THREADS environment variable to increase the number of threads for static content deployment.

>[!NOTE]
>
>You can validate your project configuration for optimal deployment by [running the ideal state wizard](smart-wizards.md#verifying-an-ideal-configuration).
