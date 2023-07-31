---
title: ECE-Tools release notes
description: See a list of the latest improvements to the ECE-Tools package.
recommendations: noDisplay, catalog
last-substantial-update: 2023-07-31
exl-id: a464b940-c56e-4a7c-9948-559539e25361
---
# ECE-Tools release notes

The [ece-tools](https://github.com/magento/ece-tools) package is a set of scripts and tools designed to manage and deploy Cloud projects. These release notes describe the latest improvements to this package, which is part of the [Cloud Tools Suite for Commerce](cloud-tools-suite.md).

>[!NOTE]
>
>See [Upgrade ECE-Tools](../dev-tools/update-package.md) for information about updating to the latest release of the `ece-tools` package.

The `ece-tools` package uses the following release versioning sequence: `200<major>.<minor>.<patch>`

The release notes include:

-  ![new icon](../../assets/new.svg) New features
-  ![fix icon](../../assets/fix.svg) Fixes and improvements

<!--Add release notes below-->

## v2002.1.15 {#latest}

Release date: July 31, 2023

-  ![fix icon](../../assets/fix.svg) **Error codes**—Updated error code schema and error code document generator.
-  ![fix icon](../../assets/fix.svg) **Validator for custom Redis model**-Updated the validator for custom Redis backend models. [See the example for cache configuration](../environment/variables-deploy.md#cache_configuration).
-  ![fix icon](../../assets/fix.svg) **Validator for RabbitMQ**-Added support for RabbitMQ 3.11
-  ![fix icon](../../assets/fix.svg) **Fixed the wrong link**-Fixed the wrong link to the onboarding documentation in the welcome email template.

## v2002.1.14

Release date: March 10, 2023

-  ![new icon](../../assets/new.svg) **PHP**—Added support for PHP 8.2.
-  ![new icon](../../assets/new.svg) **Validators for Services**—Updated validators for Commerce 2.4.6 required services: MariaDB 10.6, Redis 7.0, PHP 8.2, OpenSearch 2.x, and RabbitMQ 3.9.
-  ![fix icon](../../assets/fix.svg) **ece-tools db-dump**—Fixed an issue that caused the `db-dump` operation to stop prematurely.

## v2002.1.13

Release date: October 27, 2022

-  ![new icon](../../assets/new.svg) **Added support for Adobe I/O Events for Adobe Commerce**. Extension developers can now use the [Adobe I/O Events](https://developer.adobe.com/events/docs/) framework to send Commerce event information from Cloud instances to their applications written for [Adobe App Builder](https://developer.adobe.com/app-builder/docs/overview/). Adobe I/O Events for Adobe Commerce is in Partner Preview.<!-- CEXT-932 -->
-  ![new icon](../../assets/new.svg) **Validator for OPcache configuration**—Added a validator to check the OPcache configuration for excluded paths.<!-- MCLOUD-9485 -->
-  ![fix icon](../../assets/fix.svg) **Fixed an issue with GraphQL cache configuration**—Now ECE-Tools keeps the GraphQL `id_salt` value in `cache` configuration in the `app/etc/env.php` file.<!-- MCLOUD-9486 -->

## v2002.1.12

Release date: September 13, 2022

-  ![new icon](../../assets/new.svg) **Enable `synchronous_replication`**—ECE-Tools sets `synchronous_replication=>true` in the `app/etc/env.php` file when `MYSQL_USE_SLAVE_CONNECTION` is enabled. This configuration affects only Commerce 2.4.6+. See the `MYSQL_USE_SLAVE_CONNECTION` variable description in the [Deploy variables](../environment/variables-deploy.md#mysql_use_slave_connection).<!-- MCLOUD-9142 -->
-  ![new icon](../../assets/new.svg) **OpenSearch**—Added functionality to configure and set the `opensearch` engine for the next Adobe Commerce release 2.4.6. See [Set up OpenSearch service](../services/opensearch.md).<!-- MCLOUD-9236 -->

## v2002.1.11

Release date: August 4, 2022

-  ![fix icon](../../assets/fix.svg) **ElasticSuite Validator and OpenSearch**—Fixed ElasticSuite integrity check validator issue when OpenSearch is installed.<!-- MCLOUD-8767 -->
-  ![fix icon](../../assets/fix.svg) **Return types for deploy commands**—Fixed return types for deploy commands.<!-- AC-3208 -->
-  ![fix icon](../../assets/fix.svg) **[!DNL RabbitMQ] issue with new Commerce 2.4.5 installation**—Fixed [!DNL RabbitMQ] crash issue on new Commerce 2.4.5. installation.<!-- MCLOUD-9059 -->

## v2002.1.10

Release date: March 31, 2022

-  ![fix icon](../../assets/fix.svg) **Elasticsearch 7.10**—Updated validators to support the 7.10 version of Elasticsearch.<!-- MCLOUD-8548 -->

## v2002.1.9

Release date: March 10, 2022

-  ![new icon](../../assets/new.svg) **OpenSearch**—Added support for OpenSearch for Adobe Commerce versions 2.4.4, 2.4.3-p2, and 2.3.7-p3.<!-- MCLOUD-8296 -->
-  ![new icon](../../assets/new.svg) **PHP**—Added support for PHP 8.1.
-  ![fix icon](../../assets/fix.svg) **symfony/process**—Added the compatibility with symfony/process ^5.3.<!-- MCLOUD-8283 -->

-  ![new icon](../../assets/new.svg) **Consumer multiple processes**—Added a `multiple_processes` option so that you can specify the number of processes to spawn for each consumer. See the `CRON_CONSUMERS_RUNNER` variable description in the [Deploy variables](../environment/variables-deploy.md#cron_consumers_runner).<!-- MCLOUD-8295 -->
-  ![new icon](../../assets/new.svg) **OpenSearch scheme and full host path**—Added the ability to configure an Elasticsearch scheme and full host path.
-  ![fix icon](../../assets/fix.svg) **AWS S3**—Changed the method of AWS S3 enablement.
-  ![fix icon](../../assets/fix.svg) **Fix driver_options reader**—Added reading driver_options configuration for DB connection from the `env.php` file by `ece-tools` for validators.<!-- MCLOUD-8420 -->

## v2002.1.8

Release date: October 25, 2021

-  ![new icon](../../assets/new.svg) **Alternative dump location**—Added the `--dump-directory` option so that you can choose a target directory for a DB dump. Now `/app/var/dump-main` is the default target directory for a DB dump. See [Snapshots and backup management: Dump your database](../storage/database-dump.md)<!-- MCLOUD-8063 -->
-  ![fix icon](../../assets/fix.svg) **Update Monolog**—Updated the minimum version required for the `monolog` package to `^2.3`.<!-- ACMP-1263 -->
-  ![fix icon](../../assets/fix.svg) **Update Symfony**—Updated the Symfony dependencies to be compatible with Adobe Commerce 2.4.4.<!-- ACMP-1533 -->
-  ![fix icon](../../assets/fix.svg) **Feature/resolve autoload**—Fixed an issue when deploying to an integration environment and seeing the `CRITICAL: [9] Required configuration is missed in autoload section of composer.json file.` error.<!-- https://github.com/magento/ece-tools/pull/799 -->

## v2002.1.7

Release date: July 29, 2021

**Configuration updates**—

-  ![new icon](../../assets/new.svg) Added support for Composer 2.0.<!--MCLOUD-8003-->

-  ![fix icon](../../assets/fix.svg) **Updated composer requirements for `symphony/console`**—Updated the ECE-Tools `composer.json` version requirements for the `symphony/console` package to fix an issue that caused the `di:compile` commands to fail with the following error: `Incompatible argument type: Required type: int. Actual type: string`<!--MC-42919-->

-  ![fix icon](../../assets/fix.svg) Updated the end-of-life software checks (`eol.yaml`) to include Elasticsearch 7.9.x.<!--MCLOUD-7938-->

## v2002.1.6

Release date: April 20, 2021

-  ![new icon](../../assets/new.svg) **Redis authentication credentials**—Added the ability to read Redis authorization credentials from the `relationships` property during the deploy phase.<!--MCLOUD-7694-->

-  ![new icon](../../assets/new.svg) **Elasticsearch authorization credentials**—Added the ability to read Elasticsearch authorization credentials from the `relationships` property during the deploy phase.<!--MCLOUD-7695-->

-  ![new icon](../../assets/new.svg) **Dedicated session storage service**—Added `redis-session` as a second option for session storage. You can use the `redis-session` service to store session information and use the `redis` service for cache to provide better performance.<!--MCLOUD-7698-->

-  ![new icon](../../assets/new.svg) **Deprecated SPLIT_DB messages**—Added validator warning and critical messages for the deprecated `SPLIT_DB` option for Adobe Commerce 2.4.2 and its removal in Adobe Commerce 2.5.0.<!--MCLOUD-7806-->

-  ![fix icon](../../assets/fix.svg) **Elasticsearch version from relationships**—Fixed Service validator to retrieve the correct version of Elasticsearch from the `relationships` properties in Cloud Docker and integration environments.<!--MCLOUD-7572-->

-  ![fix icon](../../assets/fix.svg) **Flexible Redis port validation**—Redis can now validate the port in a custom cache connection from the `server` URL. For example, you can add your port number to your server URL as follows: `server: 'tcp://rfs-store-simple-page-cache:26379'`. This helps prevent validation errors where the `port` option is either missing or incorrect.<!--MCLOUD-7722-->

-  ![fix icon](../../assets/fix.svg) **Upgrading to Adobe Commerce 2.4.2**—Fixed the issue that required users to manually run `bin/magento setup:upgrade` to make their sites operational after upgrading to Adobe Commerce 2.4.2.<!--MCLOUD-7776-->

## v2002.1.5

Release date: February 1, 2021

-  ![new icon](../../assets/new.svg) **Remote storage**—Added the `REMOTE_STORAGE` environment variable to enable Cloud Projects for remote storage of media files using a storage service, such as AWS S3. This configuration option is part of the ECE-Tools package, but is not supported on Adobe Commerce on cloud infrastructure.<!--MCLOUD-7153-->

-  ![new icon](../../assets/new.svg) **New cloud:config:validate command**—Added command `php vendor/bin/ece-tools cloud:config:validate` to validate the `.magento.env.yaml` configuration before pushing changes to the remote Cloud environment.<!--MCLOUD-7120-->

-  ![new icon](../../assets/new.svg) **Flushing the opcache**—Added support for the `opcache.enable_cli` PHP option to flush the OPcache before running the deploy hook. This configuration resets the cache configuration to ensure that the current configuration settings are applied on each deployment.<!--MCLOUD-7015-->

-  ![new icon](../../assets/new.svg) **Validation of Aurora DB**—Updated the database service validation so that it is compatible with the Aurora database.<!--MCLOUD-7269-->

-  ![new icon](../../assets/new.svg) **New SCD_NO_PARENT environment variable**—Added the `SCD_NO_PARENT` environment variable (for Adobe Commerce >=2.4.2) to manage the generation of static content for parent themes.<!--MCLOUD-7284-->

-  ![fix icon](../../assets/fix.svg) **Memory limits and commands**—Fixed an issue where `php vendor/bin/ece-tools` commands would not work if the size of the `cloud.log` file exceeded the PHP memory_limit. Instead of reading the entire `cloud.log` file into memory, we now only read a smaller subset of data from the log file.<!--MCLOUD-7275--><!--MCLOUD-7400-->

-  ![fix icon](../../assets/fix.svg) **Custom database connections**—Fixed a `.magento.env.yaml` configuration issue in which custom database connections defined for `DATABASE_CONFIGURATION` were not used. The connection settings were not being added to `app/etc/env.php`.<!--MCLOUD-7426-->

-  ![fix icon](../../assets/fix.svg) **Empty error logs**—Fixed an issue that caused deployments to fail if the `cloud.error.log` was empty.<!--MCLOUD-7296-->

-  ![fix icon](../../assets/fix.svg) **MariaDB 10.3 validation**—Fixed validation of MariaDB 10.3 for Adobe Commerce 2.3.6-p1.<!--MCLOUD-7416-->

-  ![fix icon](../../assets/fix.svg) **Cache:flush logging**—Improved log entries to indicate the start and finish of the `cache:flush` step.<!--MCLOUD-7503-->

## v2002.1.4

Release date: November 19, 2020

-  ![fix icon](../../assets/fix.svg) Fixed an issue that caused deployment failure when the search engine specified in the `SEARCH_CONFIGURATION` environment variable is a value other than `elasticsearch`.<!--MCLOUD-7283-->

## v2002.1.3

Release date: November 9, 2020

**Infrastructure updates**—

-  ![new icon](../../assets/new.svg) Added ECE-Tools support for the read-only `pub/static` directory when static content is set to deploy in the build stage.<!--MC-37699-->

-  ![new icon](../../assets/new.svg) Added support for Elasticsearch 7.9 and Redis 6 for compatibility with upcoming Adobe Commerce releases.<!--MCLOUD-7191-->

-  ![fix icon](../../assets/fix.svg) Updated the ECE-Tools `composer.json` to add a required dependency for the Quality Patches Tool. This fixes a circular dependency that existed between the ECE-Tools and magento-cloud-patches packages.<!--MCLOUD-6910-->

**Validation and log improvements**—

-  ![new icon](../../assets/new.svg) Added search-engine validation to ensure that `elasticsearch` is set for Adobe Commerce on cloud infrastructure 2.4 and later. If the validation fails, the deployment is stopped with a critical error message that suggests fixes for the issue. See [Critical Errors, Deploy stage](../dev-tools/error-reference.md#deploy-stage).<!--MCLOUD-6937-->

-  ![new icon](../../assets/new.svg) Added Elasticsearch validation to check the compatibility between the Elasticsearch service version and the Adobe Commerce version.<!--MCLOUD-7193-->

-  ![new icon](../../assets/new.svg) Updated the Elasticsearch compatibility error message to show the versions of Elasticsearch that are compatible with the Adobe Commerce Elasticsearch module. The error message now provides the specific Elasticsearch versions to install in your Cloud infrastructure so that it is compatible with the Elasticsearch module used by your version of Adobe Commerce. See [Warning Errors, Deploy stage](../dev-tools/error-reference.md#deploy-stage-1).<!--MCLOUD-6698-->

-  ![new icon](../../assets/new.svg) Added warning errors `2026` and `2027` for invalid `MAGE_MODE` environment variable setting. The only valid value is `production`. Before this fix, `MAGE_MODE` could be set to `developer` without deployment errors, only to cause errors later when trying to write to read-only files. See [Warning Errors](../dev-tools/error-reference.md#warning-errors).<!--MCLOUD-6708-->

-  ![fix icon](../../assets/fix.svg) Fixed validation for Redis, RabbitMQ, and MySQL services to ensure that these versions are compatible with the Adobe Commerce version. Valid versions of these services are now written to the `cloud.log`.<!--MCLOUD-7098-->

-  ![fix icon](../../assets/fix.svg) Updated the `cloud.log` to include the concurrent requests limit for sending requests during cache warmup. This value is configured in the [WARM_UP_CONCURRENCY](../environment/variables-post-deploy.md#warm_up_concurrency) post-deploy variable.<!--MCLOUD-5563-->

**CLI command updates**—

-  ![new icon](../../assets/new.svg) Added CLI commands (`cloud:config:create` and `cloud:config:update`) to create and update the `.magento.env.yaml` file with a configuration that can include one or more build, deploy, and post-deploy variables. See [Create configuration file from CLI](../environment/configure-env-yaml.md#create-configuration-file-from-cli).<!--MCLOUD-7072-->

**Environment variable updates**—

-  ![new icon](../../assets/new.svg) Added the [SKIP_COMPOSER_DUMP_AUTOLOAD](../environment/variables-build.md#skip_composer_dump_autoload) build variable. Setting the variable to `true` stops the application from running the `composer dump-autoload` command during a Cloud Docker for Commerce installation. The variable is only relevant to Cloud Docker for Commerce containers with writable file systems (created for testing and development using `./vendor/bin/ece-docker build:compose --with-test`). With such installations, skipping the `composer dump-autoload` command prevents errors when running other commands that try to access files from a deleted `generated` directory.<!--MCLOUD-6939-->

## v2002.1.2

Release date: August 5, 2020

**Validation and log improvements**—

-  ![new icon](../../assets/new.svg) Added the `schema.error.yaml` file that includes all error and warning notifications that can occur during the build, deploy, and post-deploy process along with suggestions for resolving the errors. The information in this file is also available in the _Cloud Guide for Commerce_. See [Error message reference for ece-tools](../dev-tools/error-reference.md).<!--MCLOUD-5878-->

-  ![new icon](../../assets/new.svg) Changed the Cloud error log (`/var/log/cloud.error.log`) entries to JSON format to make the log easier to parse programmatically.<!--MCLOUD-5879-->

-  ![new icon](../../assets/new.svg) Added additional error checks to build, deploy, and post-deploy processing and improved existing checks:

   -  Error code 2026—Failed to restore some data generated during the build phase to the mounted directories

   -  Error code 3004—Cannot create backup files

   -  Error code 102—Added additional checks for issues that occur when the `env.php` file is not writable <!--MCLOUD-6221-->

-  ![new icon](../../assets/new.svg) Added the **QUALITY_PATCHES** environment variable to specify one or more quality patches to apply during the deployment process. See [Build variables](../environment/variables-build.md#quality_patches).<!--MCLOUD-6375-->

## v2002.1.1

Release date: June 25, 2020

-  ![new icon](../../assets/new.svg) **Infrastructure updates**—

   -  ![new icon](../../assets/new.svg) **Logging improvements**—Improved log-tracking capability by assigning exit codes to critical deploy errors and exposing the exit codes in error message notifications and log events. See [Error message reference for ece-tools](../dev-tools/error-reference.md).<!-- MCLOUD-5637, 5531-->

   -  ![new icon](../../assets/new.svg) Improved the process for database dumps (`vendor/bin/ece-tools db-dump`) and updated log messages to clarify that the database dump operation switches the application to maintenance mode, stops consumer queue processes, and disables cron jobs before the dump begins.<!--MCLOUD-5324, MCLOUD-2062-->

   -  ![fix icon](../../assets/fix.svg) Fixed an issue to ensure that the project URL is updated correctly when deploying to Staging and Production environments. Now, `ece-tools` uses the URL for the route with the `primary:true` attribute set in the project route configuration. See [Deploy variables](../environment/variables-deploy.md#update_urls).<!--MCLOUD-5883-->

   -  ![fix icon](../../assets/fix.svg) Updated the `generate.xml` build scenario workflow for applying patches. Patches must be applied earlier to update Adobe Commerce to fix any issues that might cause the `di:compile` and `module:refresh` steps to fail.<!--MCLOUD-5941-->

   -  ![fix icon](../../assets/fix.svg) Fixed an issue in the installation process that incorrectly returns the `Crypt key missing` error. The `crypt/key` value is generated automatically during the installation.<!--MCLOUD-6120-->

-  ![new icon](../../assets/new.svg) **Service updates**—

   -  ![new icon](../../assets/new.svg) Added support for PHP 7.4 and MariaDB 10.4.<!--MAGECLOUD-2957, MCLOUD-4144-->

-  ![new icon](../../assets/new.svg) **Environment variable updates**—

   -  ![new icon](../../assets/new.svg) Added the **SCD_USE_BALER** variable to enable the Baler module for JavaScript bundling during the Adobe Commerce on cloud infrastructure build process. See the variable description in the [build variables](../environment/variables-build.md#scd_use_baler).<!-- MCLOUD-3456, MCLOUD-3457-->

   -  ![new icon](../../assets/new.svg) Added the **REDIS_BACKEND** environment variable to configure the Redis backend model for Redis cache for Adobe Commerce 2.3.5 or later. See the variable description in the [deploy variables](../environment/variables-deploy.md#redis_backend).<!--MCLOUD-5721, MCLOUD-5865-->

-  ![new icon](../../assets/new.svg) **CLI command updates**—

   -  ![new icon](../../assets/new.svg) Updated the following CLI commands with an option for more detailed logging:

      -  `app:config:dump`
      -  `app:config:import`
      -  `module:enable`

      The logging level for each call is determined by the configuration of the [`VERBOSE_COMMANDS`](../environment/variables-build.md#verbose_commands) variable in the `.magento.env.yaml` file.<!--MCLOUD-3503-->

-  ![new icon](../../assets/new.svg) **Validation improvements**—

   -  ![new icon](../../assets/new.svg) **Elasticsearch 7.x compatibility checks**—Updated Elasticsearch validation for Elasticsearch 7.x software compatibility checks.<!--MCLOUD-5542-->

   -  ![new icon](../../assets/new.svg) **Updated service version and EOL validation checks**—Updated validation to check installed service versions against Adobe Commerce 2.4. requirements.<!--MCLOUD-6144-->

   -  ![fix icon](../../assets/fix.svg) Fixed a validation issue so that the following post-deploy warning message displays only if the `post-deploy` hook configuration is missing from the `.magento.app.yaml` file:

      ```text
      Your application does not have the "post_deploy" hook enabled.
      ```
      
      <!--MCLOUD-4077-->

   -  ![new icon](../../assets/new.svg) **Added validation for Zend Framework dependencies**—Added composer dependency validation for the Zend Framework which has migrated to the Laminas project. If the required dependencies are missing, the following error message displays during the build process.

      ```text
      Required configuration is missing from the autoload section of the composer.json file.
      Add ("Laminas\Mvc\Controller\Zend\": "setupsrc/ Zend/Mvc/Controller/") to
      the `autoload -> psr-4` section. Then, re-run the "composer update" command locally, and
      commit the updated composer.json and composer.lock files.
      ```

      See [Verify Zend Framework dependencies](../development/commerce-version.md#verify-zend-framework-composer-dependencies).<!--MCLOUD-4094-->

   -  ![new icon](../../assets/new.svg) **Added validation for `env.php` file and data**—Added checks for the `env.php` file and data during the install and upgrade process.<!--MCLOUD-5991-->

      -  If the `env.php` file is missing from the installation, and the `crypt/key` value is not specified in the `.magento.app.yaml` file, the deployment fails with the following notification:

         ```text
         The crypt/key key value does not exist in the ./app/etc/env.php file or the CRYPT_KEY cloud environment variable``Missing crypt key for upgrading Magento`.
         ```

      -  If the installation does not include the `env.php` file, or the configuration contains only one cache type, the `cron:enable` command runs during the upgrade process to restore the file with all `cache_types`. The following notification is added to the log:

         ```text
         Magento state indicated as installed but configuration file app/etc/env.php was empty or did not exist.
         Required data will be restored from environment configurations and from the .magento.env.yaml file.
         ```

## v2002.1.0

Release date: February 6, 2020

-  ![new icon](../../assets/new.svg) **Infrastructure updates**—

   -  ![new icon](../../assets/new.svg) **Added separate package for Cloud Docker for Commerce**—Decoupled the Docker package from the `ece-tools` package to maintain code quality and provide independent releases. Updates and fixes related to `ece-tools` are managed from the [magento-cloud-docker](https://github.com/magento/magento-cloud-docker) GitHub repository.<!--MAGECLOUD-2927-->

   -  ![new icon](../../assets/new.svg) **Updated patching capabilities**—Moved the patching functionality from the ECE-Tools package to a separate [magento-cloud-patches](https://github.com/magento/magento-cloud-patches) package. During deployment, `ece-tools` uses the new package to apply patches. See [Cloud patches release notes](cloud-patches.md).<!--MAGECLOUD-4567-->

   -  ![new icon](../../assets/new.svg) **Updated Composer dependencies**—Updated the `composer.json` file for Adobe Commerce on cloud infrastructure with a dependency for the `magento/magento-cloud-docker` package. Now, `ece-tools` includes dependencies for all packages in the [`Cloud Tools Suite for Commerce`](cloud-tools-suite.md). These packages are installed and updated automatically when you install or update `ece-tools`.

-  ![new icon](../../assets/new.svg) **Support for scenario-based deployments**—<!--MAGECLOUD-4101-->

   -  ![new icon](../../assets/new.svg) Now you can customize the build, deploy, and post-deploy processes using XML configuration files to override or customize the default configuration.

   -  ![new icon](../../assets/new.svg) **Changed the `hooks` configuration in `.magento.app.yaml`**—We updated the `hooks` configuration format to support scenario-based deployments. The legacy format from earlier ECE-Tools 2002.0.x release is still supported. However, you must update to the new format to use the scenario-based deployment feature. See [Scenario-based deployments](../deploy/scenario-based.md#add-scenarios-using-build-and-deploy-hooks).

>[!NOTE]
>
>Before updating to ECE-Tools version 2002.1.0, review the [backward   incompatible changes](backward-incompatible-changes.md) to learn about changes that might require you to   update Adobe Commerce on cloud infrastructure project configuration or processes.

-  ![new icon](../../assets/new.svg) **Service updates**—

   -  ![new icon](../../assets/new.svg) Added support for PHP 7.3.<!--MAGECLOUD-4022-->

   -  ![new icon](../../assets/new.svg) Added support for RabbitMQ 3.8.<!--MAGECLOUD-4674-->

   -  ![new icon](../../assets/new.svg) Added validation to check installed service versions against the EOL date for each service. Now, customers receive a notification if a service version is within three months of the EOL date, and a warning if the EOL date is in the past.<!--MAGECLOUD-4076-->

   -  ![fix icon](../../assets/fix.svg) Fixed an Elasticsearch configuration issue to ensure that the correct Elasticsearch settings are configured in all environments.<!--MAGECLOUD-4474-->

>[!NOTE]
>
>See [Service versions](../services/services-yaml.md#service-versions) for a list of services used in Adobe Commerce on cloud infrastructure and their version compatibility with the Cloud template.

-  ![new icon](../../assets/new.svg) **Environment variable updates**—

   -  ![new icon](../../assets/new.svg) Extended the functionality of the `WARM_UP_PAGES` environment variable to support cache preloading for specific product pages. See the expanded definition in the [post-deploy variables](../environment/variables-post-deploy.md#warm_up_pages) topic.<!--MAGECLOUD-4444-->

   -  ![new icon](../../assets/new.svg) Added the `ERROR_REPORT_DIR_NESTING_LEVEL` environment variable to simplify error report data management in the `<magento_root>/var/report/` directory. See the variable description in the [build variables](../environment/variables-build.md#error_report_dir_nesting_level) topic.

   -  ![fix icon](../../assets/fix.svg) Removed the `SCD_EXCLUDE_THEMES`, `STATIC_CONTENT_THREADS`,`DO_DEPLOY_STATIC_CONTENT`, and `STATIC_CONTENT_SYMLINK` environment variables. See [Backward incompatible changes](backward-incompatible-changes.md#environment-configuration-changes).<!--MAGECLOUD-4407, MAGECLOUD-3873-->

   -  ![fix icon](../../assets/fix.svg) Fixed an issue in the Elastic Suite configuration process so that the default configuration is overwritten as expected when you configure the `ELASTICSUITE_CONFIGURATION` deploy variable without the `_merge` option.<!--MAGECLOUD-4388-->

-  ![new icon](../../assets/new.svg) **CLI command updates**—

   -  ![new icon](../../assets/new.svg) **New cron command**—You can now manually manage cron processing in your Adobe Commerce on cloud infrastructure environment using the `cron:disable` and `cron:enable` commands. Use the disable command to stop all active cron processes and disable all cron jobs. Use the enable command to re-enable cron jobs when you are ready. See [Disable cron jobs](../application/crons-property.md#disable-cron-jobs).

   -  ![new icon](../../assets/new.svg) **Improved error reporting**—Added better logging for CLI command failures that occur during ECE-Tools processing.<!--MAGECLOUD-4849-->

   -  ![new icon](../../assets/new.svg) **Remove deprecated build commands**— Removed the following build commands: `m2-ece-build`, `m2-ece-deploy`, `m2-ece-scd-dump`, and renamed `ece-tools docker` commands to `ece-docker`. See [Backward incompatible changes](backward-incompatible-changes.md)<!--MAGECLOUD-4392-->

-  ![new icon](../../assets/new.svg) Removed the deprecated `build_options.ini` file and added validation to fail the build if the file exists. Use the [.magento.env.yaml](../environment/configure-env-yaml.md) file to configure build options.

-  ![fix icon](../../assets/fix.svg) Fixed an issue that caused the build process to fail when the `config.php` file is empty.<!--MAGECLOUD-4127-->

## 2002.0.23

Release date: February 27, 2020

-  ![fix icon](../../assets/fix.svg) Fixed a compatibility issue with `ece-tools` 2002.0.x releases that prevented on-demand static content generation from completing successfully in production mode.

## Older releases

See the [release notes archive](cloud-release-archive.md) for version 2002.0.22 and earlier.
