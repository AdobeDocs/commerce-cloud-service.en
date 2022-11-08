---
title: Release notes archive for ece-tools
description: Learn about archived improvements for ece-tools.
hide: yes
hidefromtoc: yes
---

# Release notes archive for ece-tools

>[!NOTE]
>
>These release notes provide information and updates for `ece-tools` v2002.0.22 and later. See [Release notes for Cloud Suite](cloud-tools.md) to get the latest updates for `ece-tools` and other Cloud packages.

## v2002.0.22

The `ece-tools` 2002.0.22 release changes the structure of the `ece-tools` package to decouple the release of `Adobe Commerce on cloud infrastructure` patches from the ECE-Tools release. Starting with this release, patches and critical fixes will be delivered using the [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) package, which is a new dependency for the `ece-tools` package. We made these changes to reduce complexity for scheduling release updates and working with community contributions.

-  ![new icon](../../assets/new.svg) **Changes to the ECE-Tools package**

   -  ![new icon](../../assets/new.svg) Moved the Adobe Commerce patches from the `ece-tools` package to a new [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) composer package.

   -  ![new icon](../../assets/new.svg) Updated the `composer.json` file for the `ece-tools` package to add a dependency for the `magento/magento-cloud-patches` v1.0.0 package.

   -  ![fix icon](../../assets/fix.svg) Fixed an issue that caused the `ece-tools` patching process to break when applying patch sets on top of security-only releases, starting with version 2.3.2-p2 and later. This issue was introduced by the new versioning scheme adopted for [security-only patches](https://devdocs.magento.com/guides/v2.3/release-notes/bk-release-notes.html#security-only-patches).<!--MAGECLOUD-4661-->

-  ![fix icon](../../assets/fix.svg) **Patches and critical fixes**–Update your Cloud environments with `ece-tools` version 2002.0.22 to apply the following patches and critical fixes. These patches are included in the `magento/magento-cloud-patches` v1.0.0 package.

   -  ![fix icon](../../assets/fix.svg) **Page Builder security patches for 2.3.1.x and 2.3.2.x releases**–Fixes an issue in Page Builder preview that allows unauthenticated users to access some templating methods that can be used to trigger arbitrary code execution over the network (RCE) resulting in global information leaks. This issue can occur when using unsupported versions of Page Builder with Adobe Commerce versions 2.3.1 and 2.3.2.<!--MAGECLOUD-4649-->

   -  ![fix icon](../../assets/fix.svg) **MSI patches**–Fixes issues that caused indexing errors and performance issues when using default inventory settings for managing stock.<!--MAGECLOUD-4428-->

   -  ![fix icon](../../assets/fix.svg) **Backward Compatibility of new Mail Interfaces**-Fixes a backward incompatibility issue caused by the `Magento\Framework\Mail\EmailMessageInterface` PHP interface introduced in Adobe Commerce v2.3.3. In the scope of this patch, the new `EmailMessageInterface` inherits from the old `MessageInterface`, and Adobe Commerce core modules are reverted to depend on `MessageInterface`.<!--MAGECLOUD-4422-->

   -  ![fix icon](../../assets/fix.svg) **Catalog pagination does not work on Elasticsearch 6.x**–Fixes a critical issue with search result pagination that affects customers using Elasticsearch 6.x as the catalog search engine.<!--MAGECLOUD-4448-->

## v2002.0.21

-  ![new icon](../../assets/new.svg) **Docker updates**—

   -  ![new icon](../../assets/new.svg) **New Docker Images**—Supported by versions 2.3.3 and later<!-- MAGECLOUD-3345 -->

      -  PHP version 7.3.<!-- MAGECLOUD-4017 -->

      -  Varnish Cache 6.2.0<!-- MAGECLOUD-4017 -->

   -  ![new icon](../../assets/new.svg) Added support to apply custom hook configuration specified in `.magento.app.yaml` in the Docker environment. Previously, the Docker environment supported only the default hook configuration.<!-- MAGECLOUD-3505-->

   -  ![new icon](../../assets/new.svg) Docker ENV files are no longer generated during the Docker build, and the `docker:config:convert` command is deprecated. The corresponding data is now stored in the `docker-compose.yml` file.<!-- MAGECLOUD-3816-->

   -  ![new icon](../../assets/new.svg) **Updated PHP image**–Added Node.js to the PHP Docker image to support node, npm, and grunt-cli capabilities.<!-- MAGECLOUD-3953 -->

-  ![new icon](../../assets/new.svg) **Environment variable updates**–

   -  ![new icon](../../assets/new.svg) Added the **LOCK_PROVIDER** deploy variable to configure the lock provider which prevents the launch of duplicate cron jobs and cron groups. See the variable description in the [deploy variables](../environment/variables-deploy.md#lock_provider) topic.<!-- MAGECLOUD-4052 -->

   -  ![new icon](../../assets/new.svg) Added the **CONSUMERS_WAIT_FOR_MAX_MESSAGES** environment variable to configure how consumers process messages from the message queue when using the `CRON_CONSUMERS_RUNNER` environment variable to manage cron jobs. See the variable description in the [deploy variables](../environment/variables-deploy.md#consumers_wait_for_max_messages) topic.<!-- MAGECLOUD-4071 -->

   -  ![fix icon](../../assets/fix.svg) Fixed an issue that can cause database deadlock errors when the `consumers_runner` cron job starts multiple instances of the same consumer on different nodes. Now, if you have enabled the [**CRON_CONSUMERS_RUNNER**](../environment/variables-deploy.md#cron_consumers_runner) deploy variable in your environment, the `consumers_runner` job uses the `single-thread` option to start one instance of each consumer on only one node.<!-- MAGECLOUD-3913 -->

   -  ![fix icon](../../assets/fix.svg) Fixed an issue affecting [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) functionality that uses a default store URL. Now, if the `config:show:default-url` command cannot fetch a base URL, then the URL from the MAGENTO_CLOUD_ROUTES variable is used.<!-- MAGECLOUD-3866 -->

-  ![new icon](../../assets/new.svg) Updated the logging information returned by the `module:refresh` command. Now, you can see a detailed list of enabled modules in the `cloud.log` file.<!-- MAGECLOUD-2514 -->

-  ![new icon](../../assets/new.svg) Improved version compatibility validation and warning notifications for compatibility issues between Adobe Commerce version and installed services, such as Elasticsearch, [!DNL RabbitMQ], Redis, and DB.<!-- MAGECLOUD-3535 -->

-  ![new icon](../../assets/new.svg) Added support for RabitMQ version 3.8.<!-- MAGECLOUD-4674-->

-  ![new icon](../../assets/new.svg) Updated interactive validations for service compatibility to reflect supported versions for the new Adobe Commerce 2.3.3 and 2.2.10 releases. See [System requirements](https://devdocs.magento.com/guides/v2.4/install-gde/system-requirements.html) in the _Installation guide_ for recommended versions.<!-- MAGECLOUD-4018 -->

-  ![fix icon](../../assets/fix.svg) Improved the log message returned when the cron job management process in the deploy phase tries to stop a cron job that has already finished to clarify that this issue is not an error. Changed the log level from `INFO` to `DEBUG`.<!-- MAGECLOUD-3653-->

-  ![fix icon](../../assets/fix.svg) Fixed an issue when running the `setup:upgrade` command that did not interrupt the deployment process when a failure occurred during the `app:config:import` task.<!-- MAGECLOUD-3806 -->

-  ![new icon](../../assets/new.svg) Changed the default log level for the file handler to `debug` to reduce the amount of detail in the log displayed in the Project Web Interface, while still providing detailed information for debugging.<!-- MAGECLOUD-3871 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that caused an error with static content deployment during build. After an installation and `ece-tools` config dump, an error occurred if there was no locale specified for the admin user in the `config.php` file. Now, there is a default locale for the admin user in the `config.php` file.<!-- MAGECLOUD-3957 -->

-  ![fix icon](../../assets/fix.svg) Fixed an `Undefined index error` that occurs when a `magento-cloud` CLI command fails in an environment that is not configured with a secure URL (https). Now, the ECE-Tools package uses the base URL (http) if the secure URL is not available.<!-- MAGECLOUD-4009 -->

## v2002.0.20

-  ![new icon](../../assets/new.svg) **Docker Updates**—

   -  ![new icon](../../assets/new.svg) You can now perform functional testing using the `ece-tools` package in the Docker environment. See [application testing](https://devdocs.magento.com/cloud/docker/docker-test-magecloud-pkg-code.html).<!-- MAGECLOUD-3129/3684 -->

   -  ![new icon](../../assets/new.svg) Added support for configuring PHP modules using the `.magento.app.yaml` file. Any [PHP Extensions specified in the `.magento.app.yaml` file](https://devdocs.magento.com/cloud/project/magento-app-php-application.html#php-extensions) become available in the Docker PHP containers.<!-- MAGECLOUD-3357 -->

   -  ![new icon](../../assets/new.svg) There are new commands available to improve the Docker command line experience. See the [`bin/magento-docker` section of the Docker reference](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli).<!-- MAGECLOUD-3569 -->

   -  ![new icon](../../assets/new.svg) Added the ability to use Mutagen.io to synchronize files during development between the local host and Docker.<!-- MAGECLOUD-3559 -->

   -  ![fix icon](../../assets/fix.svg) Corrected the default path when using the Docker environment. Now, when you use SSH to log in to the Docker container, you are at the project root in the `/app` directory, as expected.<!-- MAGECLOUD-3582 -->

   -  ![fix icon](../../assets/fix.svg) Updated the Sodium library from version 1.0.11 to version 1.0.18, and updated the Sodium PHP extension.<!-- MAGECLOUD-3832 -->

      >[!WARNING]
      >
      >Adobe Commerce on cloud infrastructure customers must [Submit an Adobe Commerce Support ticket](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) to upgrade the libsodium package on Pro Production and Staging environments prior to upgrading to Adobe Commerce 2.3.2. Currently, you cannot upgrade Starter environments to Adobe Commerce 2.3.2.

   -  ![fix icon](../../assets/fix.svg) Added the `analysis-icu` and the `analysis-phonetic` Elasticsearch plugins to all Docker images.<!-- MAGECLOUD-3446 -->

   -  ![fix icon](../../assets/fix.svg) Improved validations: When using options for the `docker:build` command, you must provide a value when using an option. Also, added validation for the Node version when using the `docker:build run` command.<!-- MAGECLOUD-3486 & MAGECLOUD-3678 -->

-  ![new icon](../../assets/new.svg) **Environment variable updates**—

   -  ![new icon](../../assets/new.svg) Added support for database table prefixes using the [DATABASE_CONFIGURATION environment variable](../environment/variables-deploy.md#database_configuration).<!-- MAGECLOUD-2901 -->

   -  ![new icon](../../assets/new.svg) Added the **FORCE_UPDATE_URLS** deploy variable to update base URLs when deploying to Pro and Starter production and staging environments. See the definition in the [deploy variables](../environment/variables-deploy.md#force_update_urls) content.<!-- MAGECLOUD-3602 -->

   -  ![new icon](../../assets/new.svg) Added the **TTFB_TESTED_PAGES** post-deploy variable to configure _Time to First Byte_  page tests to check application performance on sites deployed to Cloud infrastructure. See the variable description in [post-deploy variables](../environment/variables-post-deploy.md).<!-- MAGECLOUD-3643 -->

   -  ![fix icon](../../assets/fix.svg) Fixed an issue with multi-threaded SCD, which caused random failures in static content deployment. The workaround involved setting the **SCD_THREADS** variable to `1`. You can now increase the count as needed. See the definitions in the [deploy variables](../environment/variables-deploy.md#scd_threads) and the [build variables](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3611 -->

   -  ![fix icon](../../assets/fix.svg) You can configure the **WARM_UP_PAGES** environment variable to cache single pages, multiple domains, and multiple pages. See the expanded definition in the [post-deploy variables](../environment/variables-post-deploy.md#warm_up_pages) content.<!-- MAGECLOUD-3258 -->

-  ![fix icon](../../assets/fix.svg) Added the `pub/static/.htaccess` file to the exclude list. [Fix submitted by Björn Kraus of PHOENIX MEDIA GmbH](https://github.com/magento/ece-tools/pull/455).<!-- MAGECLOUD-3545/Github#455 -->

-  ![fix icon](../../assets/fix.svg) Fixed an error when all validation messages were showing as `Critical` if at least one critical level validator returned an error.<!-- MAGECLOUD-3178 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that caused a deployment failure if the base URL did not exist in the database.<!-- MAGECLOUD-3075 -->

-  ![new icon](../../assets/new.svg) Added a new **`env:config:show` command** to the `ece-tools` package that displays environment services, routes, or variables. See [Services, routes, and variables](https://devdocs.magento.com/cloud/reference/ece-tools-reference.html#services-routes-and-variables). [Feature submitted by Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/486).<!-- MAGECLOUD-3451 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that caused a critical error when attempting to install Adobe Commerce 2.2.6 or earlier with `ece-tools` develop after shell refactoring.<!-- MAGECLOUD-3665 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that caused Adobe Commerce 2.1.x and 2.2.x installations to fail with a warning about using a deprecated version of Carbon.<!-- MAGECLOUD-3704 -->

-  ![fix icon](../../assets/fix.svg) Decreased the `cloud.log` log level for shell output from `info` to `debug`.<!-- MAGECLOUD-3277 -->

-  ![fix icon](../../assets/fix.svg) Added the `--remove-definers (-d)` option to the `ece-tools db-dump` command to remove definers from the dump file.<!-- MAGECLOUD-3510 -->

## v2002.0.19

-  ![fix icon](../../assets/fix.svg) Fixed an issue that overwrites the `env.php` file during a deploy, resulting in a loss of custom configurations. This update ensures that Adobe Commerce on cloud infrastructure updates the `env.php` file with every deployment, while preserving custom configurations.<!-- MAGECLOUD-3668 -->

## v2002.0.18

-  ![new icon](../../assets/new.svg) **Docker Updates**—

   -  ![new icon](../../assets/new.svg) Now, the Docker environment supports the cron configuration defined in the [crons property of the .magento.app.yaml file](https://devdocs.magento.com/cloud/project/magento-app-properties.html#crons).<!-- MAGECLOUD-3150 -->

   -  ![new icon](../../assets/new.svg) **New Docker Container**—Added a [TLS termination proxy container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) to facilitate the Varnish SSL termination over HTTPS.<!-- MAGECLOUD-2890 -->

   -  ![new icon](../../assets/new.svg) **New Docker Image**—Added a Node.js image to support Gulp and other capabilities, such as Jasmine JS Unit Testing.<!-- MAGECLOUD-3345 -->

   -  ![new icon](../../assets/new.svg) **Docker build modes**—Now you can choose to launch the Docker environment in [Production mode or Developer mode](https://devdocs.magento.com/cloud/docker/docker-launch.html#set-the-launch-mode). Developer mode supports active development with full, writable filesystem permissions.<!-- MAGECLOUD-3152/3511 -->

   -  ![fix icon](../../assets/fix.svg) Fixed an issue that caused Docker deploy to fail with a `Name or service not known` error if the cache is configured for a service that is not available. Now, you can remove a service from the [`.magento/services.yaml` file](https://devdocs.magento.com/cloud/project/services.html). The Docker configuration generator updates the service in the `docker/config.php.dist` file automatically.<!-- MAGECLOUD-3369 -->

   -  ![new icon](../../assets/new.svg) Added interactive validations for service compatibility. Now, if a requested service is incompatible with the Adobe Commerce version or other services, the _interactive mode_ prompts the user with a message and a choice to continue. See the [Service versions](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers) available for Docker. Use the `-n` option to skip the interactivity for CICD purposes.<!-- MAGECLOUD-3251 -->

   -  ![fix icon](../../assets/fix.svg) Fixed an issue with the Docker compose `db-dump` command that erased existing dumps.<!-- MAGECLOUD-3366 -->

   -  ![fix icon](../../assets/fix.svg) Fixed an issue that assigned Redis `session`, `default`, and `page_cache` cache storage to the same database ID.<!-- MAGECLOUD-3172 -->

-  ![new icon](../../assets/new.svg) **Environment variable updates**—

   -  ![new icon](../../assets/new.svg) The new **ELASTICSUITE\_CONFIGURATION** environment variable retains your customized service settings between deployments. See the definition in the [deploy variables](../environment/variables-deploy.md#elasticsuite_configuration) content.<!-- MAGECLOUD-3205 -->

   -  ![new icon](../../assets/new.svg) Added the **SCD_MAX_EXECUTION_TIMEOUT** environment variable so you can increase the time to complete the static content deployment from the `.magento.env.yaml` file. See the definition in the [deploy variables](../environment/variables-deploy.md#scd_max_execution_time), the [build variables](../environment/variables-build.md#scd_max_execution_time), and the [global variables](../environment/variables-global.md#scd_max_execution_time).<!-- MAGECLOUD-2822 -->

      -  ![new icon](../../assets/new.svg) Added the **MAGENTO_CLOUD_LOCKS_DIR** environment variable to configure the path to the mount point for the lock provider on the cloud infrastructure. The lock provider prevents the launch of duplicate cron jobs and cron groups. This variable is supported on Adobe Commerce version 2.2.5 and later and automatically configured. See the definition in [Cloud variables](../environment/variables-cloud.md).<!-- MAGECLOUD-3135 -->

      -  ![fix icon](../../assets/fix.svg) Changed the **SCD_THREADS** environment variable default values to automatically determine the optimal value based on the detected CPU thread count. See the updated definitions in the [deploy variables](../environment/variables-deploy.md#scd_threads) and the [build variables](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3382 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue with a patch for DB Isolation Mechanism that caused an error when upgrading to Adobe Commerce on cloud infrastructure version 2002.0.16.<!-- MAGECLOUD-3383 -->

-  ![fix icon](../../assets/fix.svg) Added a patch that replaces _Google Image Charts_ with _Image-Charts_. See the DevBlog article [Google Image Charts deprecation and update for M1](https://community.magento.com/t5/Magento-DevBlog/Google-Image-Charts-deprecation-and-update-for-M1/ba-p/125006).<!-- MAGECLOUD-3456 -->

-  ![fix icon](../../assets/fix.svg) Added validation for the [SEARCH_CONFIGURATION variable](../environment/variables-deploy.md#search_configuration). Deploy fails when the 'engine' option is not set and `_merge` is not required.<!-- MAGECLOUD-3470 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that exposed sensitive data after an exception occurs. Now the sensitive information is masked appropriately.<!-- MAGECLOUD-3525 -->

-  ![fix icon](../../assets/fix.svg) Improved the fault-tolerant settings of the Magento Open Source package. In the case when Adobe Commerce cannot read data from the Redis `slave` instance, a reading is made from the Redis `master` instance. See [REDIS_USE_SLAVE_CONNECTION](../environment/variables-deploy.md#redis_use_slave_connection).<!-- MAGECLOUD-2899 -->

## v2002.0.17

>[!NOTE]
>
>The `ece-tools` version 2002.0.17 includes an important security patch. See [Tech Resources: Magento Open Source Patches](https://magento.com/tech-resources/download#download2288).

-  ![new icon](../../assets/new.svg) **Service updates**—Supported by the following Adobe Commerce versions: 2.2.8 and later 2.2.x, 2.3.1 and later 2.3.x

   -  Added support for Elasticsearch version 6.x.<!-- MAGECLOUD-3196 -->

   -  Added support for Redis version 5.0.

-  ![new icon](../../assets/new.svg) **New Docker images**—Added the following services to the Docker build:

   -  Elasticsearch 6.5<!-- MAGECLOUD-3196 -->

   -  Redis 5.0<!-- MAGECLOUD-3223 -->

-  ![new icon](../../assets/new.svg) **New environment variable**—Previously, there was a hard-coded timeout for SCD compression. Now you can configure the SCD compression timeout using the **SCD_COMPRESSION_TIMEOUT** environment variable. See the definitions in the [build variables](../environment/variables-build.md#scd_compression_timeout) and the [deploy variables](../environment/variables-deploy.md#scd_compression_timeout) content.<!-- MAGECLOUD-2870 -->

-  ![fix icon](../../assets/fix.svg) Added the `--use-rewrites` option to the install command so that it uses web server rewrites for generated links in the storefront and Admin access to improve security and customer experience.<!-- MAGECLOUD-3246 -->

-  ![fix icon](../../assets/fix.svg) Added timestamps to the `var/log/install_upgrade.log` file so that it shows dates for installation and upgrade events.<!-- MAGECLOUD-2895 -->

## v2002.0.16

-  ![new icon](../../assets/new.svg) **Docker updates**—

   -  Now, the default service configuration generated in the Docker environment is the same as the default configuration in the Cloud template.<!-- MAGECLOUD-3025 -->

   -  You can send mail from your Docker environment using the `sendmail` service.<!-- MAGECLOUD-2907 -->

   -  Added the ability to [configure Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) to debug in the Cloud Docker environment.<!-- MAGECLOUD-2891 -->

   -  Fixed an issue with web service permissions when generating the `docker-compose.yml` file.<!-- MAGECLOUD-2883 -->

-  ![new icon](../../assets/new.svg) **Upgrade improvement**—Added validation to confirm that the `autoload` property in the `composer.json` file contains required configuration changes before upgrading to Adobe Commerce v2.3. See [Upgrade version](https://devdocs.magento.com/cloud/project/project-upgrade.html).<!-- MAGECLOUD-2392 -->

-  ![new icon](../../assets/new.svg) The compression process in deploying static content now includes all assets—natively generated or customized—and occurs during the build phase at the beginning of the [`build:transfer` section](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks). Previously, the compression process occurred before applying custom minification and bundling of static assets. [Fix submitted by Rafael Garcia Lepper from Tryzens Limited](https://github.com/magento/ece-tools/pull/413).<!-- MAGECLOUD-3104 -->

-  ![fix icon](../../assets/fix.svg) Fixed a database connection error that occurred during deployment immediately after configuring an additional database and service relationship. Also, this fix addresses an issue that occurred during the configuration process of Commerce Reporting for Starter. For Starter, this upgrade is a "must have" for using Commerce Reporting.<!-- MAGECLOUD-3035 -->

-  ![fix icon](../../assets/fix.svg) Fixed a validation issue with the database configuration that caused the deploy process to fail.<!-- MAGECLOUD-3003 -->

-  ![fix icon](../../assets/fix.svg) Updated the constraint with the appropriate version of the `symfony/yaml` package to use with [PHP constants](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants). Constant parsing does not work when using a `symfony/yaml` package version earlier than 3.2. [Fix submitted by Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/404).<!-- MAGECLOUD-2956 -->

-  ![new icon](../../assets/new.svg) **Environment configuration check**—Added validation to check the PHP version and warn users if they are not using the latest recommended version.<!--MAGECLOUD-2903-->

-  ![fix icon](../../assets/fix.svg) Fixed an issue with processing malformed JSON variables. Now, if a JSON variable causes a syntax error, a warning appears in the `cloud.log` file and deployment continues using the default variable.<!-- MAGECLOUD-2851 -->

-  ![fix icon](../../assets/fix.svg) Fixed a connection error that occurred during deployment immediately after disabling the Redis service.<!-- MAGECLOUD-2747 -->

-  ![new icon](../../assets/new.svg) **Logging changes**—Updated the [log level](../environment/log-handlers.md#log-levels) from `Info` to `Notice` for the following build and deploy process events:<!--MAGECLOUD-2925-->

   -  Begin and end of the process for reconciling installed modules in `composer.json` with shared configuration settings in the `app/etc/config.php` file

   -  Begin and end of the configuration validation process

   -  Begin and end of the `setup:di:compile` process for generating classes

-  ![new icon](../../assets/new.svg) **New environment variables**—

   -  **[RESOURCE_CONFIGURATION deploy variable](../environment/variables-deploy.md#resource_configuration)**—Use this variable to map a resource name to a database connection.<!-- MAGECLOUD-3026 & MAGECLOUD-2963-->

   -  **[X_FRAME_CONFIGURATION global variable](../environment/variables-global.md#x_frame_configuration)**—Use this variable to change the `X-Frame-Options` header configuration for rendering a Adobe Commerce page in a `<frame>`, `<iframe>`, or `<object>`.<!-- MAGECLOUD-3048 -->

-  ![fix icon](../../assets/fix.svg) **Environment variable updates**—Changed the following environment variables:

   -  **[WARM_UP_PAGES](../environment/variables-post-deploy.md)**—Added the capability to preload the cache for specified pages on all domains defined for a Adobe Commerce store. Previously, if your site was configured with multiple domains, the post-deploy process failed to preload the cache for the specified pages on non-default domains and returned the following error in the post-deploy log: `ERROR: Warming up failed: <uri>`<!-- MAGECLOUD-2466 -->

   -  **SCD_COMPRESSION_LEVEL**—Updated the documentation and the sample `.magento.env.yaml` file with the correct default values for SCD compression level. See the definitions in the [build variables](../environment/variables-build.md#scd_compression_level) and the [deploy variables](../environment/variables-deploy.md#scd_compression_level) content.<!-- MAGECLOUD-2823 -->

   -  **SCD_EXCLUDE_THEMES**——This environment variable is deprecated. Use the [SCD_MATRIX](../environment/variables-build.md#scd_matrix) to control theme configuration.<!--MAGECLOUD-2882-->

   -  **SCD\_MATRIX**—Fixed the validation process to prevent a problem that occurred when the SCD_MATRIX ignored a theme value that contained different character cases. See the definitions in the [build variables](../environment/variables-build.md#scd_matrix) and the [deploy variables](../environment/variables-deploy.md#scd_matrix) content.<!-- MAGECLOUD-2904 -->

   -  **ADMIN variables**—<!-- MAGECLOUD-2573/MAGECLOUD-2848 -->

      -  Improved security when managing credentials for the Admin user using environment variables. You can no longer use the ADMIN_EMAIL, ADMIN_USERNAME, and ADMIN_PASSWORD environment variables to override admin credentials during upgrades. If you cannot access the Admin panel, use the _Forgot password_ feature or the `admin:user:create` CLI command to create a new admin user. See [Access your Admin panel](https://devdocs.magento.com/cloud/onboarding/onboarding-tasks.html#admin).

      -  ADMIN_EMAIL is no longer required when upgrading or applying patches.

## v2002.0.15

-  ![new icon](../../assets/new.svg) **Docker updates**—

   -  Now the Docker generator uses the services specified in the `.magento.app.yaml` and `.magento/services.yaml` configuration files when [building your Docker environment](https://devdocs.magento.com/cloud/docker/docker-config.html). You can choose a different service version using build parameters.<!-- MAGECLOUD-2888 -->

   -  Added PHP 7.2 image—Added support for PHP 7.2 in Cloud Docker; updated the [Launch Docker configuration](https://devdocs.magento.com/cloud/docker/docker-config.html) to include the `docker:build --php` option to specify the version of PHP compatible with your version of Adobe Commerce.<!-- MAGECLOUD-2799 -->

   -  Added a [Cron container](https://devdocs.magento.com/cloud/docker/docker-containers-cli.html#cron-container) based on the PHP-CLI image.<!-- MAGECLOUD-2565 -->

   -  Added the following services to the Docker build:

      -  [!DNL RabbitMQ] 3.5 and 3.7<!-- MAGECLOUD-2567 & 2889-->

      -  ElasticSearch 1.7, 2.4, and 5.2<!-- MAGECLOUD-2569 & 2887 -->

      -  Redis 3.2 and 4.0<!-- MAGECLOUD-2886 -->

-  ![new icon](../../assets/new.svg) **Configure with PHP constants**—Added support for [PHP constants](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants) in the `.magento.env.yaml` configuration file.<!-- MAGECLOUD- 2575 -->

-  ![new icon](../../assets/new.svg) **New environment variable**—By default, only the Production environment has Google Analytics enabled. You can enable Google Analytics on the Staging and Integration environments using the  [ENABLE_GOOGLE_ANALYTICS environment variable](../environment/variables-deploy.md#enable_google_analytics).<!--MAGECLOUD-2879-->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that removed customized cron configurations from the `env.php` file after a redeployment. Now, custom cron configurations safely remain in the `env.php` file.<!-- MAGECLOUD-2923 -->

-  ![fix icon](../../assets/fix.svg) Fixed inconsistencies in the messages and [log levels](../environment/log-handlers.md#log-levels) for build, deploy, and post-deploy phases. Increased beginning and ending log message levels from **info** to **notice** for all phases and sub-phases. Added beginning and ending log messages, where appropriate.<!-- MAGECLOUD-2919 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue involving cron processes that prevented the start of the post-deploy phase, when configured. Now, if you have the post-deploy hook enabled, the cron processes are enabled again at the beginning of the post-deploy phase.<!-- MAGECLOUD-2862 -->

-  ![fix icon](../../assets/fix.svg) Resolved an issue that prevented a successful installation of Adobe Commerce when specifying a custom database configuration. Previously, the installation process used the database configuration from the [MAGENTO_CLOUD_RELATIONSHIP variable](../environment/variables-cloud.md) even if you designated customized connection information in the [DATABASE_CONFIGURATION environment variable](../environment/variables-deploy.md#database_configuration).<!--MAGECLOUD-2736-->

-  ![fix icon](../../assets/fix.svg) Corrected the `config:dump` command so that it includes each website locale in the `system` section of the `config.php` file.<!--MAGECLOUD-2740-->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that resulted in _warm-up_ errors during the post-deploy phase by correcting the source base URL reference.<!--MAGECLOUD-2797-->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that generated files improperly during the `setup:di:compile` process, which affected the Amazon Pay module.<!--MAGECLOUD-2850-->

## v2002.0.14

-  ![new icon](../../assets/new.svg) **Verify Ideal State**—The `ideal-state` wizard now verifies the current configuration during each deployment and provides clear instructions for updating the configuration to achieve a faster, zero-downtime deployment.<!--MAGECLOUD-2372-->

-  ![fix icon](../../assets/fix.svg) **PCI Compliance**—Updated the messaging protocols for Adobe Commerce on cloud infrastructure to require Transport Layer Security (TLS) version 1.2 when connecting with third-party messaging services. If you are using a message service that does not support TLS version 1.2, you must upgrade your service. Otherwise, the following error message displays when your Adobe Commerce application tries to connect to the message server to send an email: `Unable to connect via TLS`.<!--MAGECLOUD-2521-->

-  ![new icon](../../assets/new.svg) **Deployment improvement**—Added validation to warn customers if a Staging or Production environment has `dev`, `debug`, or `debug_logging` options enabled to prevent performance issues caused by excessive logging activity.<!--MAGECLOUD-2517-->

-  ![fix icon](../../assets/fix.svg) **Deployment fixes**—

   -  Now maintenance mode is enabled at the start of the deploy phase and disabled at the end. If the deployment fails, the site remains in maintenance mode until the deployment issues are resolved. Previously, the site returned to production mode even if the deployment failed.<!--MAGECLOUD-2603-->

      -  Reworked the deploy phase validation checks to downgrade the error level for the following deployment issues from `CRITICAL` to `WARNING` so that the deployment completes. Previously, these issues caused the deployment to fail.

      -  Environment configuration contains incorrect values for deploy or cloud variables.

   -  The Elasticsearch version on the cloud infrastructure is incompatible with the version of the elasticsearch/elasticsearch module supported by Adobe Commerce on cloud infrastructure. See the [Elasticsearch troubleshooting article](https://support.magento.com/hc/en-us/articles/360015758471-Deployment-fails-or-interrupts-with-cloud-log-error-Elasticsearch-version-is-not-compatible-with-current-version-of-magento) in the Adobe Commerce Support Knowledgebase.<!--MAGECLOUD-2600-->

   -  Fixed an issue with the shared configuration settings in the `app/etc/config.php` file that caused `recursion detected` errors during deployment.<!--MAGECLOUD-2173-->

-  ![fix icon](../../assets/fix.svg) **Cron-related fixes**—

   -  Fixed a cron scheduling issue that prevented jobs from running if you specify a cron frequency other than the default (1 minute).<!--MAGECLOUD-2602-->

   -  Fixed an issue in the deploy phase that allowed cron jobs to continue running during deployment, which can cause database locks and other critical issues. Now, all cron jobs are stopped before the deploy phase begins and restarted after the deployment completes.<!--MAGECLOUD--2537-->

   -  Fixed the cron job workflow in versions 2.2.x to unlock frozen cron jobs so that they can be stopped before beginning deployment. Previously, a frozen cron job caused the deployment to stall.<!--MAGECLOUD-2501-->

-  ![fix icon](../../assets/fix.svg) Changed the format of the `config.php` file generated by the `vendor/bin/ece-tools config:dump` command to use short array syntax and 4-space indentation to comply with Adobe Commerce coding standards.<!--MAGECLOUD-2527-->

-  ![fix icon](../../assets/fix.svg) Fixed a deployment error that occurs when the `.magento.env.yaml` contains `{{ base_url }}` and `{{ unsecure_base_url }}` placeholders for web configurations instead of the default URL configuration for a Adobe Commerce on cloud infrastructure project./<!--MAGECLOUD-2607-->

## v2002.0.13

-  ![new icon](../../assets/new.svg) **Enable zero-downtime deployment**—Now Adobe Commerce on cloud infrastructure queues requests with required database changes during deployment and applies the changes as soon as the deployment completes. Requests can be held for up to 5 minutes to ensure that no sessions are lost. See [Static content deployment options to reduce deployment downtime on Cloud](https://support.magento.com/hc/en-us/articles/360004861194-Static-content-deployment-options-to-reduce-deployment-downtime-on-Cloud).<!--MAGECLOUD-2169-->

-  ![new icon](../../assets/new.svg) **Docker Compose for Cloud**—Made the following improvements to the [Docker setup and configuration](https://devdocs.magento.com/cloud/docker/docker-config.html) process:

   -  Added a command—`docker:config:convert` to convert PHP configuration files to Docker ENV format to simplify environment configuration. Now, you copy the PHP configuration files to the Docker directory and convert them to Docker ENV files. See [Launch Docker](https://devdocs.magento.com/cloud/docker/docker-config.html).<!--MAGECLOUD-2359-->

   -  The Adobe Commerce on cloud infrastructure installation process now supports deploying to both read-only and read-write file systems to more closely emulate the Cloud file system. See [Configure Docker](https://devdocs.magento.com/cloud/docker/docker-config.html).<!--MAGECLOUD--2357-->

   -  **Redis service support**—Added a Redis image, which is deployed to a Docker container and configured automatically to work with your Docker installation.<!--MAGECLOUD--2442-->

   -  Now you have the DB dump capability when using the Cloud Docker [database container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#database-container). Also, you can [share files](https://devdocs.magento.com/cloud/docker/docker-containers.html#sharing-data-between-host-machine-and-container) between a host machine and a container using the `docker/mnt` directory.<!-- MAGECLOUD-2577 -->

   -  **Varnish service support**— Added a Varnish image, which is deployed automatically to a Docker container. After deployment, you can manually configure Varnish following Adobe Commerce best practices. See [Configure and use Varnish](https://devdocs.magento.com/guides/v2.3/config-guide/varnish/config-varnish.html).<!--MAGECLOUD--2358-->

   -  Secure site access—Added SSL support to access your Adobe Commerce store and Admin panel.<!--MAGECLOUD--2360-->

-  ![fix icon](../../assets/fix.svg) **Improved Adobe Commerce on cloud infrastructure extension support**—Downgraded the minimum version requirement for the guzzlehttp/guzzle package in the Adobe Commerce on cloud infrastructure [composer.json file](https://devdocs.magento.com/cloud/reference/cloud-composer.html) to version 6.2 so that the `ece-tools` package is compatible with more extensions.<!--MAGECLOUD-2205-->

-  ![new icon](../../assets/new.svg) **Apply custom changes to your Adobe Commerce application during the build phase**—We split the build phase into two separate processes so that you can use hooks to apply custom changes to the generated static content before packaging the application for deployment. The _build:generate_ process generates code, applies patches, and generates static content. The _build:transfer_ process transfers the generated code and static content to the final destination. See [Application hooks](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks).<!--MAGECLOUD-2363-->

-  ![fix icon](../../assets/fix.svg) **Environment configuration checks**—Improved validation of the environment configuration to warn customers about version incompatibilities and configuration errors before building and deploying Adobe Commerce on cloud infrastructure.

   -  Added version-specific validation to identify unsupported or deprecated environment variables and values.<!--MAGECLOUD-2183-->

   -  Added an Elasticsearch compatibility check to warn users about Elasticsearch configuration issues. Now, the deployment fails if the version of Elasticsearch service on the server is incompatible with Adobe Commerce. Previously, the deployment succeeded even if the Elasticsearch version was incompatible, which caused product catalog issues after site deployment.<!--MAGECLOUD-2389-->

      You can resolve the incompatibility by [submitting a Support ticket](https://devdocs.magento.com/cloud/trouble/trouble.html) to upgrade Elasticsearch to a compatible version, or change the Adobe Commerce configuration to specify a compatible version of the Elasticsearch PHP client.

      -  For Adobe Commerce version 2.1.x to 2.2.2, upgrade Elasticsearch to version 2.4.

      -  For Adobe Commerce version 2.2.3 and later, upgrade Elasticsearch to version 5.2.

      -  If you have Elasticsearch 1.x or 2.x and do not want to upgrade, update the Adobe Commerce Elasticsearch PHP client version requirement in composer.json to `"elasticsearch/elasticsearch": "~2.0"`.

   -  Improved validation of environment variables to identify configuration settings that can cause conflicts during the build, deploy, and post-deploy phases. For example, a warning message displays during the install and upgrade process if the global setting for static content deployment conflicts with settings on the build or deploy phase.<!--MAGECLOUD-2156-->

-  ![fix icon](../../assets/fix.svg) **Environment variable updates**—Changed the following environment variables:

   -  **[SKIP_HTML_MINIFICATION global variable](../environment/variables-global.md#skip_html_minification)**—Changed the default value to `true` to enable on-demand HTML content minification, which minimizes downtime when deploying to Staging and Production environments. This configuration is required for zero-downtime deployments.<!--MAGECLOUD-2435-->

   -  **[CLEAN_STATIC_FILES deploy variable](../environment/variables-deploy.md#clean_static_files)**—Added the capability to manage the clean static files processing for static content generated during the build phase based on the CLEAN_STATIC_FILES environment variable setting. Previously, static content files generated during the build phase were always cleaned.<!--MAGECLOUD-1506-->

-  ![fix icon](../../assets/fix.svg) **Logging**—Made the following changes to improve log messages and reduce log size:

   -  Deployment failure log entries now include the command output from the operations that cause the failures even if your environment configuration does not specify debug level logging. See [`MIN_LOGGING_LEVEL`](../environment/variables-global.md#min_logging_level).<!--MAGECLOUD-2489-->

   -  Added logging for deployment failures that occur when generated factories required by some extensions cannot be generated correctly because the file system is in a read-only state.<!--MAGECLOUD-2209-->

   -  Reduced the deploy log size and fixed formatting issues caused by setup commands that use the interactive progress bar.<!--MAGECLOUD-2402-->

   -  Eliminated unnecessary verbosity and updated the priority levels for some log statements.<!--MAGECLOUD-2227-->

-  ![fix icon](../../assets/fix.svg) **Cron-specific fixes**—

   -  Changed the default cron job configuration settings for history lifetime from 3d (4320 min) to 1h (60 min) to prevent performance issues and deployment failures that can occur when the cron queue fills too quickly.<!--MAGECLOUD-2427-->

   -  Improved the cron job management process during the deploy phase to prevent database locks and other critical issues. Now, all cron jobs stop during the deploy phase and restart after deployment completes.<!--MAGECLOUD-2445-->

   -  Fixed an issue with the locking mechanism for scheduling consumers launched by cron jobs in Adobe Commerce versions 2.2.0 and later to prevent cron jobs from launching duplicate consumers.<!--MAGECLOUD-2464-->

-  ![fix icon](../../assets/fix.svg) Fixed an issue with the [static content compression process](../environment/variables-intro.md) (`gzip`) that caused `not overwritten` and `no such file or directory` errors when referencing the compressed file during the deployment process.<!-- MAGECLOUD-2182-->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that prevented the `php ./vendor/bin/ece-tools config:dump` command from removing redundant sections from the `config.php` file during the dump process if the store locale is not specified. Now you can easily move your configuration files between environments. After you update to `ece-tools` v2002.0.13, regenerate older `config.php` files with the improved `config:dump` command. See [Configuration management for store settings](https://devdocs.magento.com/cloud/live/sens-data-over.html).<!--MAGECLOUD-2444-->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that caused an error during the deploy phase if the route configuration in the `.magento/routes.yaml` file redirects from an [apex](https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp/) domain to a `www` domain.<!--MAGECLOUD-2556-->

-  ![fix icon](../../assets/fix.svg) Fixed an issue with the `_merge` option for the [`SEARCH_CONFIGURATION`](../environment/variables-deploy.md#search_configuration) variable that caused incorrect merge results if you do not include the `engine` parameter in the updated `.magento.env.yaml` configuration file. Now, the merge operation correctly overwrites only the values you specify in the updated `.magento.env.yaml` without requiring you to set the `engine` parameter.<!--MAGECLOUD-2520-->

-  ![fix icon](../../assets/fix.svg) Fixed a Redis configuration issue that incorrectly enabled session locking for Adobe Commerce on cloud infrastructure versions 2.2.1 and later, which can cause slow performance and timeouts. Now, session locking is disabled by default. The issue was caused by a change in the default behavior of the `disable_locking` parameter introduced in v1.3.4 of the Redis session handler package. See [colinmollenhour/php-redis-session-abstract package](https://github.com/colinmollenhour/php-redis-session-abstract).<!-- MAGECLOUD-2515-->

## v2002.0.12

-  ![new icon](../../assets/new.svg) **Docker Compose for Cloud**—Added a command—`docker:build`—to generate a [Docker Compose](https://devdocs.magento.com/cloud/docker/docker-config.html) configuration from the Cloud `ece-tools` repository.<!-- MAGECLOUD-2250 -->

-  ![new icon](../../assets/new.svg) **Change Locales**—Now you can change store locale without the exporting and importing configuration process. While the application is in Production and the SCD_ON_DEMAND is enabled, the store and admin locale options are available.<!-- MAGECLOUD-2019 -->

-  ![new icon](../../assets/new.svg) <!-- MAGECLOU-1998 -->**Site map and Robots**—Created a [workflow](../store/robots-sitemap.md) to add a `robots.txt` file and generate a `sitemap.xml` file for a single domain configuration without requiring a change to the infrastructure.

-  ![new icon](../../assets/new.svg) **Wizards**—Added two [wizards](../deploy/smart-wizards.md) to help you with Cloud configuration:<!-- MAGECLOUD-1910 -->

   -  `ideal-state`—configure the ideal state for minimal deployment downtime

   -  `master-slave`—configure load balancing for database and Redis

-  ![new icon](../../assets/new.svg) **Module Refresh**—Added a Cloud command—`module:refresh`—to enable modules that were disabled or not explicitly enabled, similar to the way that it is done automatically during a build.<!-- MAGECLOUD-1521 -->

-  ![new icon](../../assets/new.svg) Added the ability to choose to merge or overwrite configuration for services using the `_merge` option in [CACHE](../environment/variables-deploy.md#cache_configuration), [SESSION](../environment/variables-deploy.md#session_configuration), [QUEUE](../environment/variables-deploy.md#queue_configuration), and [SEARCH](../environment/variables-deploy.md#search_configuration) configurations.<!-- MAGECLOUD-2105 -->

-  ![new icon](../../assets/new.svg) **Environment Configuration sample file**—We added a `.magento.env.yaml` sample file to the ECE-Tools package that includes a detailed description and possible values for each environment variable.<!-- MAGECLOUD-1908 -->

   -  We also added a deep validation for the `.magento.env.yaml` configuration that prevents failures in the deployment process caused by unexpected values. When a failure occurs, you now receive a detailed error message that begins with: `Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:`<!-- MAGECLOUD-1907 -->

-  ![new icon](../../assets/new.svg) Added the following [**Environment variables**](../environment/variables-intro.md):

   -  Now you can define multiple locales for each theme using the new [SCD_MATRIX](../environment/variables-deploy.md#scd_matrix) environment variable, which reduces the amount of theme files to deploy.<!-- MAGECLOUD-1501 -->

   -   Added the [DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration) environment variable to customize your database connections for deployment.<!-- MAGECLOUD-2047 -->

   -  The new [MIN_LOGGING_LEVEL](../environment/variables-global.md#min_logging_level) variable overrides the minimum logging level for all output streams without making changes to the code.<!-- MAGECLOUD-2129 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that caused downtime between the deploy and post-deploy phase. Now, the post-deploy phase begins _immediately_ after the deploy phase ends.

-  ![fix icon](../../assets/fix.svg) Fixed an issue that did not clean the successful cron jobs, those with `status = success`, from the schedule.<!-- MAGECLOUD-2268 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue with the `post_deploy` hook that cleared the cache in the deploy phase instead of the post-deploy phase of the project.<!-- MAGECLOUD-2113 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue when using SCD with multiple locales, which generated the same `js-translation.json` file for each locale.<!-- MAGECLOUD-2034 -->

-  ![fix icon](../../assets/fix.svg) Optimized the `db:dump` command in the `ece-tools` package to avoid locking tables and increase speed.<!-- MAGECLOUD-2033 -->

## v2002.0.11

>[!NOTE]
>
>The ECE-Tools version 2002.0.11 is required for 2.2.4 compatibility.

-  ![new icon](../../assets/new.svg) **Configuring read-only connections to non-master nodes**—This release adds the ability to configure a read-only connection to a non-master node to receive read-only traffic (for  [MariaDB](../environment/variables-deploy.md#mysql_use_slave_connection)).<!--MAGECLOUD-143 -->[Redis](../environment/variables-deploy.md#redis_use_slave_connection) and for <!--MAGECLOUD-143 -->

-  ![new icon](../../assets/new.svg) **Configuration Wizard**—Added a wizard to help verify your configuration for static content deployment. See [Smart wizards](../deploy/smart-wizards.md).<!--MAGECLOUD-1910 -->

-  ![new icon](../../assets/new.svg) **Symfony Console support**—Added support for Symfony Console 4 with Adobe Commerce 2.3.<!-- MAGECLOUD-1966 -->

-  ![fix icon](../../assets/fix.svg) **Cron scheduling optimizations**—Improved the queue management and enhanced logging to help with debugging cron-related issues.<!-- MAGECLOUD-1607 -->

-  ![fix icon](../../assets/fix.svg) Deployment validation fails if an `ADMIN_EMAIL` or `ADMIN_USERNAME` value is the same as an existing administrator account.<!-- MAGECLOUD-1221 -->

-  ![fix icon](../../assets/fix.svg) Removed SOLR support for 2.2.x versions. 2.1.x versions retain the ability to enable SOLR.<!-- MAGECLOUD-1282 -->

-  ![fix icon](../../assets/fix.svg) The first installation of the Staging & Production environments of a PRO project now includes different index prefixes for ElasticSearch to prevent possible conflicts while identifying records belonging to each environment.<!-- MAGECLOUD-1489 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that interrupted the build phase for legacy architecture during static content deployment.<!-- MAGECLOUD-2021 -->

-  ![fix icon](../../assets/fix.svg) **Cron-specific Improvements**—Re-worked the cron implementation:<!-- MAGECLOUD-1607 -->

   -  Fixed an issue that caused the cron queue to fill quickly. Now it clears the outdated cron jobs in a more reliable way.

   -  Re-organized the sequence of cron jobs so that all jobs in separate threads launch prior to the general group.

   -  Improved logging to better assist in debugging cron issues.

   -  **NOTE**—This release addresses many cron-related issues. If you currently use some cron-related patches in _m2-hotfixes_, remove them.

-  ![fix icon](../../assets/fix.svg) **SCD-specific improvements**—

   -  You can use the `VERBOSE_COMMANDS` and the `SCD_COMPRESSION_LEVEL` environment variables during both _build_ and de_ploy phases.<!-- MAGECLOUD-1819 -->

   -  Fixed an issue that caused deployment to fail with a random error when encountering an unexpected value for the `SCD_COMPRESSION_LEVEL` environment variable. Improved the configuration validation to provide meaningful notifications. See [`SCD_COMPRESSION_LEVEL`](../environment/variables-build.md#scd_compression_level) for acceptable values.<!-- MAGECLOUD-2043 -->

   -  Fixed the behavior of the `SCD_COMPRESSION_LEVEL` environment variable configuration flow so the overrides work as expected.<!-- MAGECLOUD-2044 -->

   -  Fixed an issue that prevented the configuration of the `SCD_THREADS` environment variable in the `.magento.env.yaml` file _deploy_ stage.<!-- MAGECLOUD-2046 -->

## v2002.0.10

-  ![new icon](../../assets/new.svg) **Static Content Deployment (SCD)**—There is a new, alternative deployment process to generate static content when requested (on-demand). This decreases downtime and improves cache handling by generating the most critical assets.<!-- MAGECLOUD-1285 -->

   -  **New environment variable**—Added the `SCD_ON_DEMAND` global environment variable to generate static content when requested.<!-- MAGECLOUD-1738 -->

   -  **Post-deploy hook**—Added a `post_deploy` hook for the `.magento.app.yaml` file that clears the cache and pre-loads (warms) the cache _after_ the container begins accepting connections. It is available only for Pro projects that contain Staging and Production environments in the Project Web Interface and for Starter projects. Although not required, this works in tandem with the `SCD_ON_DEMAND` environment variable.<!-- MAGECLOUD-1788 -->

-  ![new icon](../../assets/new.svg) **Optimization**—Optimized moving or copying files during deployment to improve deployment speed and decrease loads on the file system.<!-- MAGECLOUD-1842 -->

-  ![new icon](../../assets/new.svg) **Deployment Logging**—Added the ability to enable Syslog and Graylog Extended Log Format (GELF) handlers for outputting logs during the deployment process. See [Logging handlers](../environment/log-handlers.md).<!-- MAGECLOUD-1751 -->

-  ![new icon](../../assets/new.svg) Added the following [**Environment variables**](../environment/variables-intro.md):

   -  `CRYPT_KEY`—Provide a cryptographic key to another environment when moving a database.<!-- MAGECLOUD-1556 -->

   -  `SKIP_HTML_MINIFICATION`—_Global_ environment variable that skips copying the static view files in the `var/view_preprocessed` directory and generates minified HTML when requested.<!-- MAGECLOUD-1621 and MAGECLOUD-1736-->

   -  `SCD_ON_DEMAND`—_Global_ environment variable to generate static content when requested.<!-- MAGECLOUD-1738 -->

   -  `WARM_UP_PAGES`—You can list the pages to use to pre-load the cache. Available in the new [Post-deploy variables](../environment/variables-post-deploy.md).

-  ![fix icon](../../assets/fix.svg) Fixed an issue that involved a locally applied patch breaking the deployment on an instance. Now, ECE-Tools can detect that a patch has been applied.<!-- MAGECLOUD-982 -->

-  ![fix icon](../../assets/fix.svg) Fixed a conflict between JavaScript bundling and GZIP functionality. Now these features work correctly together.<!-- MAGECLOUD-1735 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that caused ECE-Tools CLI commands to fail when using earlier PHP 7.0.x versions.<!-- MAGECLOUD-1744 -->

-  ![fix icon](../../assets/fix.svg) Fixed an issue that prevented static content deployment with the compact strategy in multiple threads.<!-- MAGECLOUD-1822 -->

-  ![fix icon](../../assets/fix.svg) Fixed a Redis session locking issue that caused an Admin login delay. Also, the fix is available for 2.1.x.<!-- MAGECLOUD-1853 -->

## v2002.0.9

>[!NOTE]
>
>You must [upgrade the Adobe Commerce on cloud infrastructure metapackage](../dev-tools/install-package.md#update-the-metapackage) to get this and all future updates.

-  ![new icon](../../assets/new.svg) **ece-tools**—The `ece-tools` package now supports Adobe Commerce 2.1.x.<!-- MAGECLOUD-1086 -->

-  ![new icon](../../assets/new.svg) **Redis configuration**—You can now [configure Redis](../environment/variables-deploy.md#cache_configuration) page and default cache and Redis session storage using an environment variable.<!-- MAGECLOUD-1552 -->

-  ![new icon](../../assets/new.svg) **Search, AMQP, and Redis service improvements**—We unified the service configuration flow so that it now behaves the same way for all services. Manually editing the `env.php` file to configure services is no longer supported. You must use environment variables or the `.magento.env.yaml` file instead.<!-- MAGECLOUD-1437 -->

-  ![fix icon](../../assets/fix.svg) **Environment variables**—

   -  The use of `env:STATIC_CONTENT_THREADS` was deprecated and will be removed in a future release. Use the [SCD_THREADS](../environment/variables-deploy.md#scd_threads) instead.<!-- MAGECLOUD-1507 -->

   -  The `STATIC_CONTENT_EXCLUDE_THEMES` environment variable was deprecated. You must use the `SCD_EXCLUDE_THEMES` environment variable instead.<!-- MAGECLOUD-1640 -->

-  ![fix icon](../../assets/fix.svg) **Logging**—We simplified logging around built-in patching operations.<!-- MAGECLOUD-1674 -->

-  ![fix icon](../../assets/fix.svg) We removed `developer` mode support and the `APPLICATION_MODE` environment variable because they were causing unexpected behavior.<!-- MAGECLOUD-1615 -->

-  ![fix icon](../../assets/fix.svg) We fixed an issue that was causing static content deployment failures related to Redis. Now, multi-threaded static content deployment runs as designed.<!-- MAGECLOUD-1630 -->

-  ![fix icon](../../assets/fix.svg) We fixed an issue that was preventing users from saving modifications to configuration fields in the Admin, which are marked as sensitive after running the `app:config:dump` command.<!-- MAGECLOUD-1175 -->

-  ![fix icon](../../assets/fix.svg) We added support for an earlier version of `symfony/yaml` to fix conflicts with some packages, which are not yet compatible with the latest version.<!-- MAGECLOUD-1674 -->

## v2002.0.8

>[!NOTE]
>
>We merged `vendor/magento/ece-patches` with `vendor/magento/ece-tools` in this release. You no longer need to update the `vendor/magento/ece-patches` package separately.

**New features:**

-  **Improved logging**<!-- MAGECLOUD-1253 -MAGECLOUD-1495 -->
   -  We improved log messaging to provide better explanations when the build or deploy process overrides an environment variable.
   -  You can now view installation and upgrade progress in real time. Tail the `install_update.log` file to view progress. For example,

      ```bash
      tail -f var/log/install_upgrade.log
      ```

-  **New cron command**—You can now unlock specific stuck cron jobs instead of stopping and re-launching all of them with the [`cron:unlock`](https://support.magento.com/hc/en-us/articles/360033099451) command. Not available in 2.1.<!-- MAGECLOUD-1367 -->

-  **Unified configuration file**—You can now configure build and deploy stages using a [`.magento.env.yaml`](https://devdocs.magento.com/cloud/project/magento-env-yaml.html) file.<!-- MAGECLOUD-1369 -->

-  **Backup configuration files**—The deployment process now automatically creates a backup of the `app/etc/env.php` and `app/etc/config.php` configuration files after deployment. We also added a [new CLI command](https://support.magento.com/hc/en-us/articles/360033182871) to restore these configuration files from a backup.<!-- MAGECLOUD-1372 -->

-  **Troubleshooting validation errors**—We changed the command you must use to resolve validation errors when `config.php` does not contain enough data for static content deployment. Previously, the error message instructed you to run `bin/magento app:config:dump`. Now, you must run `php ./vendor/bin/ece-tools config:dump`.<!-- MAGECLOUD-1491 -->

-  **New environment variables**—You can now use environment variables to connect custom [search](../environment/variables-deploy.md#search_configuration) and [AMQP-based](../environment/variables-deploy.md#queue_configuration) services to your site.<!-- MAGECLOUD-1410 -->

-  We implemented smart patching. Now the package applies patches based not on Adobe Commerce on cloud infrastructure version, but on patched package version.<!--MAGECLOUD-1090-->

**Resolved issues:**

-  We fixed a logging issue that was causing build errors.<!-- MAGECLOUD-1162 -->

-  We fixed an issue that was causing timeout exceptions when running deployments in interactive mode.<!-- MAGECLOUD-1389 -->

-  We fixed an issue that was causing errors when using the compact strategy for static content generation. Not available in 2.1.<!-- MAGECLOUD-1446 MAGECLOUD-1485-->

-  We fixed an issue that was preventing the deployment script from properly identifying staging and production environments.<!-- MAGECLOUD-1493 -->

-  We fixed an issue that was causing network issues to disrupt database connections and cause failures during the installation and upgrade process.<!-- MAGECLOUD-1520 -->

-  We fixed an issue preventing you from exporting the configuration files using `app:config:dump` more than once. Not available in 2.1.<!--  MAGECLOUD-1567  -->

-  We fixed a Redis session _locking_ issue that caused an _Admin_ login delay. Not available in 2.1.<!--  MAGECLOUD-1582  -->

-  We fixed an implementation issue related to versioning that was causing a conflict with other Composer-based patching modules.<!-- MAGECLOUD-1450 -->

-  We fixed an issue that was causing PHP memory issues during import.<!-- MAGECLOUD-1310 -->

-  Removed patch; fixing bug in `colinmollenhour/credis` v1.6 to enable support for Adobe Commerce on cloud infrastructure 2.2.1. Not available in 2.1.<!-- MAGECLOUD-1033 -->

## v2002.0.7

**Resolved issues:**

-  We removed `var/view_preprocessed` symlinking to fix an issue that was causing JavaScript minification conflicts.<!-- MAGECLOUD-1454 -->

## v2002.0.6

**Resolved issues:**

-  We fixed an issue that was causing `gzip` errors when a file or directory name contains spaces.<!-- MAGECLOUD-1413 -->

-  We fixed an issue that was preventing deployment scripts from properly recognizing and enabling module dependencies.<!-- MAGECLOUD-1424 -->

## v2002.0.5

**New features:**

-  **Configure a cron consumer with an environment variable**—You can now configure cron consumers using the new `CRON_CONSUMERS_RUNNER` environment variable.

-  **Configuration scanning**—We now scan for critical components during the build/deploy process and halt the process if the scan fails, which prevents unnecessary downtime due to the site being in maintenance mode.

-  **Build/deploy notifications**—We added a configuration file that you can use to [set up Slack and/or email notifications](../environment/set-up-notifications.md) for build/deploy actions in all your environments.

-  **Static content compression**—We now compress static content using [gzip](https://www.gnu.org/software/gzip/) during the build and deploy phases. This compression, coupled with Fastly compression, helps reduce the size of your store and increase deployment speed. If necessary, you can disable compression using a [build option](../environment/variables-build.md) or [deploy variable](../environment/variables-deploy.md). See the following topics for more information:

   -  [Application environment variables](../application/variables-property.md)

   -  [Static content deployment performance](../deploy/static-content.md)

   -  [Deployment process](https://devdocs.magento.com/cloud/reference/discover-deploy.html)

-  **Configuration management**—We now auto-generate an `app/etc/config.php` file in your Git repository during the build phase if it does not already exist. The auto-generated file includes only a list of modules and extensions. If the file already exists, the build phase continues as normal. If you follow [Configuration Management](../store/store-settings.md) at a later time, the commands update the file without requiring additional steps. Refer to [Deployment process](https://devdocs.magento.com/cloud/reference/discover-deploy.html) for more information.

-  **Database dumps**—We added a `magento/ece-tools` CLI command for creating database dumps in all environments. For Pro plan Production environments, this command only dumps from one of three high-availability nodes, so production data written to a different node during the dump may not be copied. We recommend putting the application in maintenance mode before doing a database dump in Production environments. See [Snapshots and backup management](https://devdocs.magento.com/cloud/project/project-webint-snap.html#db-dump) for more information.

-  **Cron interval limitations lifted**—The default cron interval for all environments provisioned in the us-3, eu-3, and ap-3 regions is 1 minute. The default cron interval in all other regions is 5 minutes for Pro Integration environments and 1 minute for Pro Staging and Production environments. To modify your existing cron jobs, edit your settings in `.magento.app.yaml` or create a support ticket for Production/Staging environments. Refer to [Set up cron jobs](../application/crons-property.md#set-up-cron-jobs) for more information.

**Resolved issues:**

-  We fixed an issue that was causing long deploy times due to the deploy process invoking the `cache-clean` operation before static content deployment.<!-- MAGECLOUD-1327 -->

-  We fixed an issue causing errors during the static content generation step of deployment on Production environments.<!-- MAGECLOUD-1322 -->

-  We fixed an issue preventing some `magento/ece-tools` commands from logging output to `stderr`.<!-- MAGECLOUD-1264 -->

-  We fixed an issue preventing base URL values in `env.php` from being updated in forked branches.<!-- MAGECLOUD-1242 -->

-  We fixed an issue causing the `magento setup:install` command to add an unsecure prefix (`http://`) to secure base URLs.<!-- MAGECLOUD-1171 -->

-  We fixed an issue preventing patch errors from causing deployment failures.<!-- MAGECLOUD-1170 -->

-  We fixed an issue preventing `ece-tools` from halting execution and throwing an exception if no patches can be applied.<!-- MAGECLOUD-1152 -->

-  We fixed an issue causing errors when loading the storefront after enabling HTML minification in the Admin.<!-- MAGECLOUD-1138 -->

## v2002.0.4

**Resolved issues:**

-  You can now [manually reset stuck cron jobs](https://support.magento.com/hc/en-us/articles/360033099451) using a CLI command in all environments via SSH access. The deployment process automatically resets cron jobs.<!-- MAGECLOUD-1355 -->

## v2002.0.3

**Resolved issues:**

-  We fixed an issue that was causing pages to time out because Redis was taking too long to read/write. You can now use the `disable_locking` parameter in Redis configurations to prevent this issue.<!-- MAGECLOUD-1311 -->

## v2002.0.2

**Resolved issues:**

-  The [!DNL RabbitMQ] configuration process now obtains all required parameters automatically.<!-- MAGECLOUD-1246 -->

## v2002.0.1

**New features:**

-  Adobe Commerce on cloud infrastructure now supports scopes and [static content deployment strategies](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-static-deploy-strategies.html). We have added the `–s` parameter with a default setting of `quick` for the static content deployment strategy. You can use the environment variable [SCD_STRATEGY](../environment/variables-deploy.md) to customize and use these strategies with your build and deploy actions. This variable supports the options `standard`, `quick`, or `compact`. If you select `compact`, we override the `STATIC_CONTENT_THREADS` value with `1`, which can slow deployment, especially in production environments. Not available in 2.1.<!--- MAGECLOUD-1057 -->

-  We have created a log file on environments to capture and compile build and deploy actions. The file is located in the `var/log/cloud.log` file inside the root application directory.<!--- MAGECLOUD-1014 & MAGECLOUD-1023 -->

**Resolved issues:**

-  Refactored the `ece-tools` package to make it compatible with Adobe Commerce on cloud infrastructure 2.2.0 and higher.<!-- MAGECLOUD-919 & MAGECLOUD-1030 -->

-  We fixed an issue that was preventing `ece-tools` from halting execution and throwing an exception if no patches can be applied.<!-- MAGECLOUD-1186 -->

-  We fixed an issue that was causing exceptions to be thrown when  dependency injection (di) compilation is skipped during builds.<!-- MAGECLOUD-1047 & MAGECLOUD-1049 -->

-  We fixed an issue that was causing the deploy process to overwrite custom Redis configurations in the `env.php` file.<!-- MAGECLOUD-1019 -->

-  We fixed an issue that was causing redirect loops due to disabled by default secure admin.<!-- MAGECLOUD-1020 -->

## v2002.0.0

>[!WARNING]
>
>This package is no longer compatible with other versions of Adobe Commerce on cloud infrastructure and **should not** be used.

### Initial release

Initial release of `ece-tools` for Adobe Commerce on cloud infrastructure 2.2.0.
