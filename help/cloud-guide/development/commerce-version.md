---
title: Upgrade Commerce version
description: Learn how to upgrade the Adobe Commerce version in the cloud infrastructure project.
feature: Cloud, Upgrade
exl-id: 87821007-4979-4a20-940b-aa3c82c192d8
---
# Upgrade Commerce version

You can upgrade the Adobe Commerce code base to a newer version. Before upgrading your project, review the [System requirements](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in the _Installation_ guide for the latest software version requirements.

Depending on your project configuration, your upgrade tasks may include the following:

-  Update services for compatibility with new Adobe Commerce versions. See [Change service version](../services/services-yaml.md#change-service-version).
-  Convert an older configuration management file.
-  Update the `.magento.app.yaml` file with new settings for hooks and environment variables.
-  Upgrade third-party extensions to the latest supported version.
-  Update the `.gitignore` file.

{{upgrade-tip}}

{{pro-update-service}}

## Upgrade from older versions

If you are beginning an upgrade from a Commerce version older than 2.1, some restrictions in the Adobe Commerce code base can affect your ability to _update_ to a specific ECE-Tools release or to _upgrade_ to the next supported Commerce version. Use the following table to determine the best path:

| Current Version   | Upgrade Path |
| ----------------- | ------------ |
| 2.1.3 and earlier | Upgrade Adobe Commerce to version 2.1.4 or later before you continue. Then perform a [one-time upgrade to install ECE-Tools](../dev-tools/install-package.md). |
| 2.1.4 – 2.1.14    | [Update ECE-Tools](../dev-tools/update-package.md) package.<br>See release notes for [2002.0.9](../release-notes/cloud-release-archive.md#v200209) and later 2002.0.x releases. |
| 2.1.15 – 2.1.16   | [Update ECE-Tools](../dev-tools/update-package.md) package.<br>See release notes for[2002.0.9](../release-notes/cloud-release-archive.md#v200209) and later. |
| 2.2.x and later   | [Update ECE-Tools](../dev-tools/update-package.md) package.<br>See release notes for[2002.0.8](../release-notes/cloud-release-archive.md#v200208) and later. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Configuration management

Older versions of Adobe Commerce, such as 2.1.4 or later to 2.2.x or later, used a `config.local.php` file for Configuration Management. Adobe Commerce version 2.2.0 and later use the `config.php` file, which works exactly like the `config.local.php` file, but it has different configuration settings that include a list of your enabled modules and additional configuration options.

When upgrading from an older version, you must migrate the `config.local.php` file to use the newer `config.php` file. Use the following steps to back up your configuration file and create one.

**To create a temporary `config.php` file**:

1. Create a copy of `config.local.php` file and name it `config.php`.

1. Add this file to the `app/etc` folder of your project.

1. Add and commit the file to your branch.

1. Push the file to your integration branch.

1. Continue with the upgrade process.

>[!WARNING]
>
>After upgrading, you can remove the `config.php` file and generate a new, complete file. You can only delete this file to replace it this one time. After generating a new, complete `config.php` file, you cannot delete the file to generate a new one. See [Configuration Management and Pipeline Deployment](../store/store-settings.md).

### Verify Zend Framework composer dependencies

When upgrading to **2.3.x or later from 2.2.x**, verify that the Zend Framework dependencies have been added to the `autoload` property of the `composer.json` file to support Laminas. This plugin supports new requirements for the Zend Framework, which has migrated to the Laminas project. See [Migration of Zend Framework to the Laminas Project](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) on the _Magento DevBlog_.

**To check the `auto-load:psr-4` configuration**:

1. On your local workstation, change to your project directory.

1. Check out your integration branch.

1. Open the `composer.json` file in a text editor.

1. Check the `autoload:psr-4` section for the Zend plugin manager implementation for controllers dependency.

   ```json
    "autoload": {
       "psr-4": {
          "Magento\\Framework\\": "lib/internal/Magento/Framework/",
          "Magento\\Setup\\": "setup/src/Magento/Setup/",
          "Magento\\": "app/code/Magento/",
          "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
       },
   }
   ```

1. If the Zend dependency is missing, update the `composer.json` file:

   -  Add the following line to the `autoload:psr-4` section.

      ```json
      "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
      ```

   -  Update the project dependencies.

      ```bash
      composer update
      ```

   -  Add, commit, and push code changes.

      ```bash
      git add -A
      ```

      ```bash
      git commit -m "Add Zend plugin manager implementation for controllers dependency for Laminas support"
      ```

      ```bash
      git push origin <branch-name>
      ```

   -  Merge changes to the Staging environment, and then to Production.

## Configuration files

Before upgrading the application, you must update your project configuration files to account for changes to the default configuration settings for Adobe Commerce on cloud infrastructure or the application. The latest defaults can be found in the [magento-cloud GitHub repository](https://github.com/magento/magento-cloud).

### .magento.app.yaml

Always review the values contained in the [.magento.app.yaml](../application/configure-app-yaml.md) file for your installed version, because it controls the way your application builds and deploys to the cloud infrastructure. The following example is for version 2.4.6 and uses Composer 2.2.21. The `build: flavor:` property is not used for Composer 2.x; see [Installing and using Composer 2](../application/properties.md#installing-and-using-composer-2).

**To update the `.magento.app.yaml` file**:

1. On your local workstation, change to your project directory.

1. Open and edit the `magento.app.yaml` file.

1. Update the PHP options.

   ```yaml
   type: php:8.2

   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.2.21'
   ```

1. Modify the `hooks` property `build` and `deploy` commands.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           composer install
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Add the following environment variables to the end of the file. 

   For Adobe Commerce 2.2.x through 2.3.x–

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

   For Adobe Commerce 2.4.x–

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

1. Save the file. Do not commit or push changes to the remote environment yet.

1. Continue with the upgrade process.

### composer.json

Before upgrading, always check that the dependencies in the `composer.json` file are compatible with the Adobe Commerce version.

**To update the `composer.json` file for Adobe Commerce version 2.4.4 and later**:

1. Add the following `allow-plugins` to the `config` section:

   ```json

   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. Add the following plugin to the `require` section:

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. Add the following component to the `extra:component_paths` section:

   ```json
   "extra": {
      "component_paths": {
         "tinymce/tinymce": "lib/web/tiny_mce_5"
      },
   },
   ```

1. Save the file. Do not commit or push changes to your branch yet.

1. Continue with the upgrade process.

## Project backup

We recommend creating a backup of your project before an upgrade. Use the following steps to back up your Integration, Staging, and Production environments.

**To back up your Integration environment database and code**:

1. Create a local backup of the remote database.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >The `magento-cloud db:dump` command runs the [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) command with the `--single-transaction` flag, which allows you to back up your database without locking the tables.

1. Back up code and media.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   Optionally, you can omit `[--media]` if you have a large number of static files that are already in source control.

**To back up your Staging or Production environment database before deploying**:

1. Use SSH to log in to the remote environment.

1. Create a database dump. To choose a target directory for the DB dump, use the `--dump-directory` option.

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   The dump operation creates a `dump-<timestamp>.sql.gz` archive file in your remote project directory. See [Back up database](../storage/database-dump.md).

## Application upgrade

Review the [service versions](../services/services-yaml.md#service-versions) information for the latest software version requirements before upgrading your application.

**To upgrade the application version**:

1. On your local workstation, change to your project directory.

1. Set the upgrade version using the [version constraint syntax](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >You must use the version constraint syntax to successfully update the `ECE-Tools` package. You can find the version constraint in the `composer.json` file for the version of the [application template](https://github.com/magento/magento-cloud/blob/master/composer.json) you are using for the upgrade.

1. Update the project.

   ```bash
   composer update
   ```

1. Add, commit, and push code changes.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Upgrade"
   ```

   ```bash
   git push origin <branch-name>
   ```

   `git add -A` is required to add all changed files to source control because of the way Composer marshals base packages. Both `composer install` and `composer update` marshal files from the base package (`magento/magento2-base` and `magento/magento2-ee-base`) into the package root.

   The files that Composer marshals belong to the new version of Adobe Commerce, to overwrite the outdated version of those same files. Currently, marshaling is disabled in Adobe Commerce, so you must add the marshaled files to source control.

1. Wait for deployment to complete.

1. Verify the upgrade in your Integration, Staging, or Production environment by using SSH to log in and check the version.

   ```bash
   php bin/magento --version
   ```

### Create a config.php file

As mentioned in [Configuration management](#configuration-management), after upgrading, you must create an updated `config.php` file. Complete any additional configuration changes through the Admin in your Integration environment.

**To create a system-specific configuration file**:

1. From the terminal, use an SSH command to generate the `/app/etc/config.php` file for the environment.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   For example for Pro, to run the `scd-dump` on the `integration` branch:

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Transfer the `config.php` file to your local workstations using `rsync` or `scp`. You can only add this file to the branch locally.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Add, commit, and push code changes.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   This generates an updated `/app/etc/config.php` file with a module list and configuration settings.

>[!WARNING]
>
>For an upgrade, you delete the `config.php` file. Once this file is added to your code, you should **not** delete it. If you must remove or edit settings, edit the file manually.

### Upgrade extensions

Review your third-party extension and module pages in Marketplace or other company sites and verify support for Adobe Commerce and Adobe Commerce on cloud infrastructure. If you must upgrade any third-party extensions and modules, Adobe recommends working in a new integration branch with your extensions disabled.

**To verify and upgrade your extensions**:

1. Create a branch on your local workstation.

1. Disable your extensions as needed.

1. When available, download extension upgrades.

1. Install the upgrade as documented by the third-party documentation.

1. Enable and test the extension.

1. Add, commit, and push the code changes to the remote.

1. Push to and test in your Integration environment.

1. Push to the Staging environment to test in a pre-production environment.

Adobe strongly recommends upgrading your Production environment _before_ including the upgraded extensions in your site launch process.

>[!NOTE]
>
>When you upgrade your application version, the upgrade process updates to the latest version of the [Fastly CDN module](../cdn/fastly.md#fastly-cdn-module-for-magento-2) automatically.

## Troubleshoot upgrade

If the upgrade failed, you receive an error message in the browser indicating that you cannot access your storefront or the Admin panel:

```terminal
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**To resolve the error**:

1. On your local workstation, change to your project directory.

1. Use SSH to log in to the remote environment.

   ```bash
   magento-cloud ssh
   ```

1. Open the `./app/var/report/<error number>` file.

1. [Examine the logs](../test/log-locations.md) and determine the source of the issue.

1. Add, commit, and push code changes.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
