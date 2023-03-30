---
title: Enable the B2B module
description: Learn how to enable the business-to-business module for Adobe Commerce on cloud infrastructure.
exl-id: 01d02ea0-1e7d-4608-adbf-1dad7f5e2182
---
# Enable the B2B module

If your customers are companies, you can install the B2B for Adobe Commerce module to extend your Adobe Commerce on cloud infrastructure Pro project to accommodate a business-to-business model. Although this topic provides information specific to installing and configuring the B2B module for Adobe Commerce on cloud infrastructure, you can find additional B2B information in the following guides:

- [Adobe Commerce B2B Developer Guide](https://developer.adobe.com/commerce/webapi/rest/b2b/)
- [Adobe Commerce B2B User Guide](https://experienceleague.adobe.com/docs/commerce-admin/b2b/guide-overview.html)

>[!TIP]
>
>Because B2B is a module for Adobe Commerce on cloud infrastructure, Adobe recommends that you deploy your Adobe Commerce application to an Integration or Staging environment before beginning.

## Install B2B module

Adobe recommends working in a development branch when adding the B2B module to your project. If you do not have a branch, see [Create a branch for development](../development/cli-branches.md#create-a-branch-for-development). When installing the B2B module, the `Magento_B2b` module name is automatically inserted in the `app/etc/config.php` file. There is no need to edit the file directly.

**To install the B2B module**:

1. On your local workstation, change to your project directory.

1. Create or check out a development branch.

1. Add the B2B module to the `require` section of the `composer.json` file.

   ```bash
   composer require magento/extension-b2b --no-update
   ```

1. Update the project dependencies.

   ```bash
   composer update
   ```

1. Add, commit, and push code changes.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Install the B2B module."
   ```

   ```bash
   git push origin <branch-name>
   ```

1. After the build and deploy finishes, use SSH to log in to the remote environment and verify that the B2B module installed.

   ```bash
   bin/magento module:status Magento_B2b
   ```

   An extension name uses the format: `<VendorName>_<ComponentName>`.

   Sample response:

   ```terminal
   Magento_B2b : Module is enabled
   ```

   If you encounter deployment errors, see [Recover from component failure](../deploy/recover-failed-deployment.md).

## Enable the B2B module

When you install the B2B module using Composer, the deployment process automatically enables the module. If you already have the B2B module installed, you can enable or disable the module using the CLI

Enable the B2B module:

```bash
bin/magento module:enable Magento_B2b
```

Sample response:

```terminal
The following modules have been enabled:
- Magento_B2b

Cache cleared successfully.
Generated classes cleared successfully. Please run the 'setup:di:compile' command to generate classes.
Info: Some modules might require static view files to be cleared. To do this, run 'module:enable' with the --clear-static-content option to clear them.
```

See [Manage extensions](extensions.md).

## Configure the B2B module

After installing the B2B for Adobe Commerce module, you must [start the message consumers](https://experienceleague.adobe.com/docs/commerce-admin/b2b/install.html#start-message-consumers) so that you can enable the _Shared Catalog_ module, and you must [enable the B2B features](https://experienceleague.adobe.com/docs/commerce-admin/b2b/enable-basic-features.html).
