---
title: Starter project workflow
description: Learn how to use the Starter development and deployment workflows.
feature: Cloud, Paas
exl-id: f334047a-1e0d-45c7-bf96-5c2964741951
---
# Starter project workflow

The Adobe Commerce on cloud infrastructure includes a single Git repository with a `master` branch for the production environment that can be branched to create a staging and multiple integration environments for testing and development work. You can have up to four active environments, including a `master` environment for your production server. See [Starter architecture](starter-architecture.md) for an overview.

For your environments, follow the [!UICONTROL Development > Staging > Production] workflow to develop and deploy your site.

-  **Production environment (live site)**—Provides a full production environment with all services built and deployed from the code on the `master` branch.
-  **Staging environment**—Provides a full staging environment that matches the production environment with all services built and deployed from a `staging` branch that you create by cloning from `master`.
-  **Integration environments**—Provides up to two active development environments that you create from the `staging` branch. The `integration` environment does not support third-party services like Fastly and New Relic.

For your branches, you can follow any development methodology. For example, you can follow an Agile methodology such as scrum to create branches for every sprint.

From each sprint, you can create branches for every user story. All the stories become testable. You can continually merge to the sprint branch and validate that branch on a continuous basis. When the sprint ends, you can merge the sprint branch to `master` to deploy all sprint changes to production without having to deal with a testing bottleneck.

## Development workflow

Development and deployment on Starter plans begin with your initial project. You create your project with the "blank site", which is an Adobe Commerce on cloud infrastructure template code repo with a fully prepared store. This creates a `master` branch with a copy of the code from your production environment.

The development workflow includes the following:

-  [Clone and branch](#clone-and-branch) from the `master` to create `staging` and development branches
-  [Develop code](#develop-code) and install extensions locally in a development branch
-  [Configure](#configure-store) your store and extension settings
-  [Generate configuration](#generate-configuration-management-files) management files
-  [Push code](#push-code-and-test) and configuration to build and deploy to the `staging` and `production` environments

![Develop and deploy workflow](../../assets/starter/workflow.png)

You also have a few optional steps to help develop and test your code and your store data:

-  [Install sample data](#optional-install-sample-data) to your store
-  [Pull production store data](#optional-pull-production-data) down to environments

This process assumes that you have set up your [local developer workspace](../development/overview.md).

### Clone and branch

For a new Starter Plan project, a `master` branch was cloned from the Adobe Commerce on cloud infrastructure Git repository. To start branching and working with code, clone the `master` branch to your local environment.

The format of the Git clone command is:

```bash
git fetch origin
```

```bash
git pull origin <environment-ID>
```

The first time you start working in branches for your Starter project, create a `staging` branch. This creates a code branch matching the `master` branch that deploys to a Staging environment to test configuration and code changes before deploying to the production environment.

Next, create branches from `staging` to develop code, add extensions, and configure third-party integrations. Anytime you develop custom code, add extensions, integrate with a third-party service, work in a development branch created from the `staging` branch. You have four active integration environments available. When you push an active branch, one of these integration environments automatically deploys your code to test.

The format of the Git branch command is:

```bash
git checkout <branch-name>
```

The format of the Cloud CLI `branch` command is:

```bash
magento-cloud environment:branch <environment-name> <parent-environment-ID>
```

![Branch from Master](../../assets/starter/branching.png)

### Develop code

Using the base branch of Adobe Commerce on cloud infrastructure code, you can start installing extensions, developing custom code, adding themes, and much more.

Use a branching strategy with your development work. Using one branch to do all of your work all at once might make testing difficult. For example, you could follow continuous integration and sprint methodologies to work:

-  Add a few extensions and configure them with your first branch
-  Push this code, test, and merge to Staging then Production
-  Fully configure your services in `services.yaml` and add a theme
-  Push this code, test, and merge to Staging then Production
-  Integrate with a third-party service
-  Push this code, test, and merge to Staging then Production

Until you have your store fully built, configured, and ready to launch. But keep reading, there are many options for your store and code configuration.

>[!NOTE]
>
>Do not complete any configurations in your local workstation yet.

![Push code from local](../../assets/starter/push-code.png)

### Configure store

When you are ready to configure your store, push all your code to the `integration` environment. Configure your store settings from the Admin for the integration environment, not in your local environment. You can find the URL by clicking **Access site** in the [!DNL Cloud Console]

For the best information on configurations, review the documentation for Adobe Commerce and the installed extensions. Here are some links and ideas that help you get started:

-  [Best practices for store configuration](../store/best-practices.md) for specific best practices in the cloud
-  [Basic configuration](https://docs.magento.com/user-guide/configuration/configuration-basic.html) for store admin access, name, languages, currencies, branding, sites, store views and more
-  [Theme](https://docs.magento.com/user-guide/design/design-theme.html) for your look and feel of the site and stores including CSS and layouts
-  [System configuration](https://docs.magento.com/user-guide/system/system.html) for roles, tools, notifications, and your encryption key for your database
-  Extension settings using their documentation

Beyond just store settings, you can further configure multiple sites and stores, configured services, and more. See [Configure your store](../store/overview.md).

### Generate configuration management files

If you are familiar with Adobe Commerce, you may be concerned about how to get your configuration settings from your database in development to the staging and production environments. Previously, you had to copy all your configuration settings down on paper or to a file, and then manually apply the settings to other environments. Or you may have dumped your database and pushed that data to another environment.

Adobe Commerce on cloud infrastructure provides a set of two [Configuration Management](../store/store-settings.md) commands that export configuration settings from your environment into a file. These commands are only available for **Adobe Commerce on cloud infrastructure 2.2 and later**.

-  `php .vendor/bin/ece-tools config:dump`—Exports only the configuration settings that you entered or modified from defaults into a configuration file. _Recommended_.
-  `php bin/magento app:config:dump`—Exports every configuration setting, including modified and default, into a configuration file.

The generated file is `app/etc/config.php`.

Generate the file in the integration environment where you configured Adobe Commerce. Step through the process of generating the file, adding it to your branch, and deploying it.

**Important notes** on Configuration Management:

-  Any configuration setting included in the file generated from the `app:config:dump` command is locked from editing, or read-only, in the deployed environment. This is one reason that Adobe recommends using the `.vendor/bin/ece-tools config:dump` command.

   For example, you install a module for Fastly in your development environment. You can only configure this module in the staging and production environment. Using the `.vendor/bin/ece-tools config:dump` command keeps those default fields editable when you deploy your development changes to the Staging and production environment.

-  The generated file can be long depending on the size of your deployment. The `.vendor/bin/ece-tools config:dump` command generates a smaller file than the file generated by the `app:config:dump` command.

If you are using Adobe Commerce version 2.2 or later, the configuration management commands provide an additional feature to protect sensitive data, like sandbox credentials for a PayPal module. During the export process, any values that contain sensitive data are exported to separate configuration file—`env.php` in the `app/etc/` directory. This file remains in your local environment and does not get copied when you push your code to another branch. You can also create environment variables with CLI commands in all Adobe Commerce on cloud infrastructure versions.

![Environment variables generate](../../assets/starter/env-variables.png)

See [Configuration Management](../store/store-settings.md).

### Push code and test

At this point, you should have a developed code branch with a configuration file (`config.local.php` or `config.php`) ready to test.

Every time you push code from your local environment, a series of build and deploy scripts run. These scripts generate new code and deploy it to the remote environment. For example, if you are pushing a development branch from your local environment to the remote branch, a matching environment updates services, code, and static content.

You can directly access this environment with a store URL, Admin URL, and SSH. These environments include a web server, database, and configured services. When ready, you can start deploying and testing in the Staging environment.

For more information, see [Deployment workflow](#deployment-workflow).

### Optional: Install sample data

If you need some example data when developing your store, you can install sample data. This data simulates an active store, including customers, products, and other data. This sample data works best with a "blank site" Adobe Commerce on cloud infrastructure template installation when creating your project. As a best practice, remove the sample data before going live. See [Install optional sample data](../test/sample-data.md).

![Install optional sample data](../../assets/starter/sample-data.png)

### Optional: Pull production data

Add all of your products, catalogs, site content, and so on, directly to the `production` environment. By adding this data to the production environment, you can provide updated prices, coupons, inventory stock, sales announcements, information about future offerings, and more for your customers. This data does not include extension configurations, which you configure in your local development branch.

As you develop features, add extensions, and design themes, having real data to work with is helpful. At any time, you can [create a database dump](../storage/database-dump.md) from the production environment and push that to your Staging and integration environments as needed.

To help export Production data as test data to use in staging and integration environments:

-  [Run the support utilities](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/run-support-utilities.html) CLI commands (Recommended) when exporting a protected backup of customer and store data using your Adobe Commerce encryption key

-  [Data Collection](https://docs.magento.com/user-guide/system/support-data-collector.html) tool for generating and exporting data

To migrate this data, see [Migrate and deploy static files and data](../deploy/staging-production.md#migrate-static-files).

![Pull and sanitize production data](../../assets/starter/data-code-process.png)

>[!NOTE]
>
>Before pushing the data to another environment, you should consider sanitizing your data. You have a couple of options including [using support utilities](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/run-support-utilities.html) or developing a script to scrub out customer data.

>[!WARNING]
>
>Do not push a database from an integration or staging environment to a production environment. If you do, the data from the integration or staging environment overwrites your live production data, including sales, orders, new and updated customers, and more.

## Deployment workflow

As detailed in the architecture information, Adobe Commerce on cloud infrastructure is Git driven. Deploying Adobe Commerce on cloud infrastructure is part of your Git push processes for branches.

When you push branched code from your local environment to the remote branch, a series of build and deploy scripts begin.

Build scripts:

-  The site in the target environment continues running during a build

-  Check and run Adobe Commerce on cloud infrastructure patches and hotfixes

-  Compile your code with a build and deploy log

-  Check for Configuration Management, if the static content deployment occurs during this phase

-  Create or use a slug of unchanged code for a quicker process

-  Provision all backend services and applications

Deploy scripts:

-  Puts your site on the target environment in Maintenance mode

-  Deploys static content if not completed during Build

-  Installs or updates Adobe Commerce on cloud infrastructure

-  Configure routing for traffic

When fully completed, your store comes back online, live, with all of your updated code and configurations.

See [Deployment process](../deploy/process.md).

### Push to Staging and test

Always push your code in iterations to the `staging` environment for full testing. The first time you use this environment, you must configure a few services, including [Fastly](/help/cloud-guide/cdn/fastly.md) and [New Relic](../monitor/new-relic-service.md). Also, configure payment gateways, shipping, notifications, and other vital services with sandbox or testing credentials.

Staging is a pre-production environment, providing all services and settings as close to production as possible. Thoroughly test every service, verify your performance testing tools, perform UAT testing as an administrator and as a customer, until you feel your store is ready for production.

See [Deploy your store](../deploy/staging-production.md).

### Push to Production

When you push to the `master` branch, you are pushing to the `production` environment. Complete configuration and testing activities in the production environment as you did in the staging environment with one important difference. In the production environment, use live credentials for configuration and testing. The moment you launch your site, customers can complete purchases, and administrators can manage the live store.

See [Deploy your store](../deploy/staging-production.md).

### Site launch

There is a clear walk-through for going live with your site. After you complete these steps, your store can serve up products in your customized theme for sale immediately.

See [Site launch](../launch/overview.md).

## Continuous integration

Following your branching and development methodologies, you can easily develop new features, configure changes, and add extensions to continuously develop and deploy updates.

All cloud infrastructure environments support continuous integration for constant updates. This workflow supports releases multiple times a day or on a set schedule according to your business needs.

-  Create development branches with future features and changes

-  Test the code in your `integration` environment

-  Deploy and test in `staging` environment

-  Deploy to the `production` environment
