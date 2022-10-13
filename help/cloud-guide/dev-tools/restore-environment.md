---
title: Restore an environment
description: Learn how to uninstall the Adobe Commerce application from a cloud infrastrucutre project and restore an environment to a stable state.
---

# Restore an environment

If you encounter issues in the Integration environment and do not have a [valid snapshot](snapshots.md), try restoring your environment using one of the following methods:

- Unistall Commerce (SSH)
- Force a redeployment
- Manually reset the database

## Uninstall Commerce

Uninstalling the Commerce application returns your environment to an original state by restoring the database, removing the deployment configuration, and clearing the `var/` subdirectories. This guidance also resets your git branch to an earlier stable state. If you do not have a recent snapshot, but you can access the remote environment using SSH, follow these steps to restore your environment:

- Disable configuration management
- Uninstall Adobe Commerce
- Reset the git branch

Uninstalling the Adobe Commerce software drops and restores the database, removes the deployment configuration, and clears the `var/` subdirectories. It is important to disable [Configuration management](https://devdocs.magento.com/cloud/live/sens-data-over.html) so that it does not automatically apply the previous configuration settings during the next deployment. Make sure that your `app/etc/` directory does not contain the `config.php` file.

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

### Reset the Git branch

Resetting your Git branch reverts the code to a stable state in the past.

To reset your branch:

1. On your local workstation, change to your project directory.

1. Review the Git commit history. Use `--reverse` to display history in reverse chronological order:

   ```bash
   git log --reverse
   ```

1. Choose a commit hash that represents the last known stable state of your code.

   To reset your branch to its original initialized state, find the very first commit that created your branch.

   ```terminal
   commit 398c8fd3a46534fc88d6de250c5d081d5be3c852
   Author: Alice Username <alice@example.com>
   Date:   Wed Apr 13 16:16:13 2021 -0500

       Init 2.4.4
   ```

1. Use the hard reset option to reset your branch.

   ```bash
   git reset --h <commit-hash>
   ```

1. Push your changes to trigger a redeploy, which reinstalls Adobe Commerce.

   ```bash
   git push --force <origin> <branch>
   ```

## Uninstall failed

If you have attempted to uninstall Adobe Commerce and the command failed or could not complete, you might need to manually reset the database.

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

1. Log out and trigger a redeploy.

   ```bash
   magento-cloud environment:redeploy
   ```

## Force a redeployment

If you have attempted to uninstall Adobe Commerce and your deployment continues to fail, you can try to manually force a redeployment.

```bash
git commit --allow-empty -m "<message>" && git push <origin> <branch>
```
