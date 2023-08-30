---
title: Optimize cloud deployment
description: Learn about ways to optimize the deployment process for Adobe Commerce on cloud infrastructure projects, including reducing downtime, static content deployment, scenario-based deployment, and smart wizards.
feature: Cloud, Deploy, SCD
exl-id: 62e5eccb-6919-4a4b-9f50-6105f9d0f3af
---
# Optimize deployment

Site performance can suffer during the deployment process. The length of time a site is in maintenance mode when deploying to a production site depends on many factors, such as environment configuration and the amount of content a site contains. The first best practice for optimizing your Cloud deployment is to [upgrade to use `ece-tools`](../dev-tools/install-package.md) to benefit from the package features, such as commands to create a backup of the database and verify environment configuration.

The following topics can help you to better understand how to optimize the deployment process:

-  [Cloud deployment process](process.md)
    There are three phases in the Cloud deployment process, and you can use the strengths and weaknesses of each phase to your advantage.

-  [Zero downtime deployment](reduce-downtime.md)
    Understand what happens during deployment and how to reduce the amount of downtime your store experiences during an update to the Production environment.

-  [Static content deployment](static-content.md)
    The best way to optimize your Cloud deployment is to control how and when to generate static content.

-  [Smart wizards](smart-wizards.md)
    The `ece-tools` package provides the smart wizard commands to quickly evaluate your project configuration.

-  [Track deployments with New Relic](../monitor/track-deployments.md)
   You can use the New Relic service to monitor deployment events and anlyze deployment impact to overall performance.
