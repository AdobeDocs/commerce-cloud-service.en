---
title: Recover from component failure
description: Learn how you can recover if a component fails to deploy properly in Adobe Commerce on cloud infrastructure.
exl-id: 4855be0c-6883-4ab1-a364-316d10e97250
---
# Recover from component failure

This topic discusses how to recover if a component fails to deploy properly. Typical examples include components that have dependencies that are not met by your remote environment, such as incompatible PHP versions.

You can recover from a failed deployment in any of the following ways:

- [Restore a snapshot](../storage/snapshots.md#restore-a-snapshot)
- Clean project and code from previous changes and redeploy

## Clean, remove, and redeploy

To clean up from the previous deployment, you may need to identify the component that was added or updated and then remove it. First, log in to the remote environment and manually clear the contents of the `var` directory. Then remove the component from the `composer.json` file and redeploy the environment.

**To clean the `var` directories**:

1. On your local workstation, change to your project directory.

1. Use SSH to log in to the remote environment.

   ```bash
   magento-cloud ssh
   ```

1. Clear the `var` directories.

   ```shell
   rm -rf var/*
   ```

1. Log out.

**To remove the component**:

1. On your local workstation, change to your project directory.

1. Clear the cache.

   ```bash
   composer clear-cache
   ```

1. Remove the component from the `composer.json` file.

   ```bash
   composer remove <component-name>:<version>
   ```

   If the following message displays, you do not need to do anything further:

   ```terminal
   Package "<name>:<version>" listed for update is not installed. Ignoring.
   ```

1. Wait while the dependencies are updated.

1. Add, commit, and push code changes.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "<message>"
   ```

   ```bash
   git push origin <environment-ID>
   ```

{{redeploy-warning}}

See more about restoring an environment without a snapshot in [Restore an environment](../development/restore-environment.md).

{{stuck-deployment-tip}}
