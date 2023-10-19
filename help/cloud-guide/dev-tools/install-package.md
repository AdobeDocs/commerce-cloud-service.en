---
title: Upgrade project to use ECE-Tools
description: Learn how to upgrade your Adobe Commerce on cloud infrastructure project to use the ECE-Tools package and take advantage of the latest fixes and features.
feature: Cloud, Install
exl-id: 820cca84-2817-4881-829f-ebb78400d8c7
---
# Upgrade project to use ECE-Tools package

Adobe deprecated the `magento/magento-cloud-configuration` and `magento/ece-patches` packages in favor of the `ece-tools` package, which simplifies many cloud processes. If you use an older Adobe Commerce on cloud infrastructure project that does _not_ contain the `ece-tools` package, then you must perform a one-time, manual _upgrade_ process to your project.

>[!WARNING]
>
>If your project contains the `ece-tools` package, you can skip the following upgrade. To verify, retrieve the Commerce version using the `php vendor/bin/ece-tools -V` command at your local project root directory.

This project upgrade process requires you to update the `magento/magento-cloud-metapackage` version constraint in the `composer.json` file at the root directory. This constraint enables updates for Adobe Commerce on cloud infrastructure metapackages—including removing deprecated packages—without upgrading your current Adobe Commerce version.

{{upgrade-tip}}

## Remove deprecated packages

Before performing an upgrade to use the `ece-tools` package, check the `composer.lock` file for the following deprecated packages:

-  `magento/magento-cloud-configuration`
-  `magento/ece-patches`

## Update the metapackage

Each Adobe Commerce version requires a different constraint based on the following:

```terminal
>=current_version <next_version
```

-  For `current_version`, specify the Adobe Commerce version to install.
-  For `next_version`, specify the next patch version after the value specified in `current_version`.

If you want to install Adobe Commerce `2.3.5-p2`, set `current_version` to `2.3.5` and the `next_version` to `2.3.6`. The constraint `">=2.3.5 <2.3.6"` installs the latest available package for 2.3.5.

You can always find the latest metapackage constraint in the [`magento-cloud` template](https://github.com/magento/magento-cloud/blob/master/composer.json).

The following example places a constraint for the Adobe Commerce on cloud infrastructure metapackage to any version greater than or equal to the current version 2.4.5 and lower than next version 2.4.6:

```json
"require": {
    "magento/magento-cloud-metapackage": ">=2.4.5 <2.4.6"
},
```

## Upgrade the project

To upgrade your project to use the `ece-tools` package, you must update the metapackage and the `.magento.app.yaml` hooks properties, and perform a Composer update.

**To upgrade project to use ece-tools**:

1. Update the `magento/magento-cloud-metapackage` version constraint in the `composer.json` file.

    ```bash
    composer require "magento/magento-cloud-metapackage":">=2.4.5 <2.4.6" --no-update
    ```

1. Update the metapackage.

   ```bash
   composer update magento/magento-cloud-metapackage
   ```

1. Modify the hook commands in the `magento.app.yaml` file.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Check for and remove the [deprecated packages](#remove-deprecated-packages). The deprecated packages can prevent a successful upgrade.

   ```bash
   composer remove magento/magento-cloud-configuration
   ```

   ```bash
   composer remove magento/ece-patches
   ```

1. It may be necessary to update the `ece-tools` package.

   ```bash
   composer update magento/ece-tools
   ```

1. Add and commit the code changes. In this example, the following files were updated:

   ```terminal
   .magento.app.yaml
   composer.json
   composer.lock
   ```

1. Push your code changes to the remote server and merge this branch with the `integration` branch.

   ```bash
   git push origin <branch-name>
   ```
