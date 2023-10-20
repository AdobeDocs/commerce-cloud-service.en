---
title: Restore an environment
description: Learn how to uninstall the Adobe Commerce application from a cloud infrastructure project and restore an environment to a stable state.
role: Developer
topic: Development
exl-id: b76bd6c3-986e-4adc-abd0-5b27db0d8a3b
---
# Restore an environment

If you encounter issues in the integration environment and do not have a [valid backup](../storage/snapshots.md), try restoring your environment using one of the following methods:

- Reset or revert the code in the Git branch
- Uninstall the Commerce application
- Force a redeployment
- Manually reset the database

{{stuck-deployment-tip}}

## Reset the Git branch

Resetting your Git branch reverts the code to a stable state in the past.

**To reset your branch**:

1. On your local workstation, change to your project directory.

1. Review the Git commit history. Use `--oneline` to show abbreviated commits on one line:

   ```bash
   git log --oneline
   ```

   Sample response:

   ```terminal
   6bf9f45 (HEAD -> master, magento/master, magento/develop, magento/HEAD, develop) Create composer.lock
   34d7434 2.4.6 upgrade
   b69803c Update composer.lock
   c1bca24 Add sample data
   ec604c3 Update magento/ece-tools
   ...
   ```

1. Choose a commit hash that represents the last known stable state of your code.

   To reset your branch to its original initialized state, find the first commit that created your branch. You can use `--reverse` to display history in reverse chronological order.

1. Use the hard reset option to reset your branch. Be careful using this command because it discards all changes since the chosen commit.

   ```bash
   git reset --hard <commit>
   ```

1. Push your changes to trigger a redeployment, which reinstalls Adobe Commerce.

   ```bash
   git push --force <origin> <branch>
   ```

## Uninstall Commerce

Uninstalling the Commerce application returns your environment to an original state by restoring the database, removing the deployment configuration, and clearing the `var/` subdirectories. This guidance also resets your git branch to an earlier stable state. If you do not have a recent backup, but you can access the remote environment using SSH, follow these steps to restore your environment:

- Disable configuration management
- Uninstall Adobe Commerce
- Reset the git branch

Uninstalling the Adobe Commerce software drops and restores the database, removes the deployment configuration, and clears the `var/` subdirectories. It is important to disable [Configuration management](../store/store-settings.md) so that it does not automatically apply the previous configuration settings during the next deployment. Make sure that your `app/etc/` directory does not contain the `config.php` file.

**To uninstall the Adobe Commerce software**:

1. On your local workstation, change to your project directory.

1. Use SSH to log in to the remote environment.

   ```bash
   magento-cloud ssh
   ```

1. Remove the configuration file.
   -  For Adobe Commerce 2.2 and later:

      ```bash
      rm app/etc/config.php
      ```

   -  For Adobe Commerce 2.1:

      ```bash
      rm app/etc/config.local.php
      ```

1. Uninstall the Adobe Commerce application.

   ```bash
   php bin/magento setup:uninstall -n
   ```

1. Confirm that Adobe Commerce was successfully uninstalled.

   The following message displays to confirm a successful uninstallation:

   ```terminal
   [SUCCESS]: Magento uninstallation complete.
   ```

1. Clear the `var/` subdirectories.

   ```bash
   rm -rf var/*
   ```

1. Log out.

>[!TIP]
>
>Optionally, it is a good practice to clean build caches.
>
>```bash
>magento-cloud project:clear-build-cache
>```

## Force a redeployment

If you have attempted to uninstall Adobe Commerce and your deployment continues to fail, you can try to manually force a redeployment.

```bash
git commit --allow-empty -m "<message>" && git push <origin> <branch>
```

## Reset the database

If you have attempted to uninstall Adobe Commerce and the command failed or could not complete, you can manually reset the database.

**To reset the database**:

1. On your local workstation, change to your project directory.

1. Use SSH to log in to the remote environment.

   ```bash
   magento-cloud ssh
   ```

1. Connect to the database.

   ```bash
   mysql -h database.internal
   ```

1. Drop the `main` database.

   ```shell
   drop database main;
   ```

1. Create an empty `main` database.

   ```shell
   create database main;
   ```

1. Delete the following configuration files.

   -  `config.php`
   -  `config.php.bak`
   -  `env.php`
   -  `env.php.bak`

1. Log out and trigger a redeployment.

   ```bash
   magento-cloud environment:redeploy
   ```

{{redeploy-warning}}
