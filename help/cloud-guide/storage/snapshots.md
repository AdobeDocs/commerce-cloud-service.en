---
title: Backup management
description: Learn how to manually create and restore a backup for your Adobe Commerce on cloud infrastructure project.
feature: Cloud, Paas, Snapshots, Storage
exl-id: 1cb00db7-2375-4761-9c07-1e20a74859e0
---
# Backup management

You can perform a manual backup of active Starter environments at any time using the **[!UICONTROL Backup]** button in the [!DNL Cloud Console] or using the `magento-cloud snapshot:create` command.

A backup or _snapshot_ is a complete backup of environment data that includes all persistent data from running services (MySQL database) and any files stored on the mounted volumes (var, pub/media, app/etc). The snapshot does _not_ include code, since the code is already stored in the Git-based repository. You cannot download a copy of a snapshot.

The backup/snapshot feature does **not** apply to the Pro Staging and Production environments, which receive regular backups for disaster recovery purposes by default. Refer to [Pro Backup & Disaster Recovery](../architecture/pro-architecture.md#backup-and-disaster-recovery) for more information. Unlike the automatic live backups on the Pro Staging and Production environments, backups are **not** automatic. It is _your_ responsibility to manually create a backup or set up a cron job to periodically create a backup of your Starter or Pro integration environments.

## Create a manual backup

You can create a manual backup of any active Starter environment and integration Pro environment from the [!DNL Cloud Console] or create a snapshot from the Cloud CLI. You must have an [Admin role](../project/user-access.md) for the environment.

**To create a backup of any Starter environment using the [!DNL Cloud Console]**:

1. Log in to the [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Select an environment from the project navigation bar. The environment must be active.
1. In the _Backups_ view, click **[!UICONTROL Backup]**. This option is not available for a Pro environment.

   ![Backup](../../assets/button-backup.png){width="150"}

**To create a backup of an integration environment using the [!DNL Cloud Console]**:

1. Log in to the [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Select an integration/development environment from the project navigation bar. The environment must be active.
1. Select the **[!UICONTROL Backup]** option in the top-right menu. This option is available for both Starter and Pro environments.
1. Click the **[!UICONTROL Yes]** button.

**To create a snapshot using the `magento-cloud` CLI**:

1. On your local workstation, change to your project directory.
1. Check out the environment branch to snapshot.
1. Create the snapshot.

   ```bash
   magento-cloud snapshot:create --live
   ```

   Alternatively, you can use the `magento-cloud backup` short command. The `--live` option leaves the environment running to avoid downtime. For a full list of options, enter `magento-cloud snapshot:create --help`.

   Sample response:

   ```terminal
   Creating a snapshot of develop-branch
   Waiting for the activity ID (User created a backup of develop-branch):

   Creating backup of develop-branch
   Created backup my-snapshot
   [============================] 45 secs (complete)
   Activity ID succeeded
   Snapshot name: my-snapshot
   ```

1. Verify the most recent snapshots.

   ```bash
   magento-cloud snapshot:list
   ```

   The list returns information about the snapshot status:

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

## Restore a manual backup

You must have [Admin access](../project/user-access.md) to the environment. You have up to **seven days** to _restore_ a manual backup. Restoring a backup does not change the code of the current git branch. Restoring a backup in this manner does not apply to Pro staging and production environments; see [Pro Backup & Disaster Recovery](../architecture/pro-architecture.md#backup-and-disaster-recovery).

Restoration times vary depending on the size of your database:

- large database (200+ GB) can take 5 hours
- medium database (150 GB) can take 2 1/2 hours
- small database (60 GB) can take 1 hour

>[!TIP]
>
>Restoring without a backup:
>
>- To roll back to previous code or remove added extensions in an environment, see [Roll back code](#roll-back-code).
>- To restore an unstable environment that does _not_ have a backup, see [Restore an environment](../development/restore-environment.md).

**To restore a backup using the [!DNL Cloud Console]**:

1. Log in to the [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Select an environment from the project navigation bar.
1. In the _Backups_ view, choose a backup from the _Stored_ list. The backup feature does **not** apply to the Pro environments.
1. In the ![More](../../assets/icon-more.png){width="32"} (_more_) menu, click **Restore**.
1. Review the Restore from backup information and click **Yes, restore**.

**To restore a snapshot using the Cloud CLI**:

1. On your local workstation, change to your project directory.
1. Check out the environment branch to restore.
1. List all available snapshots.

   ```bash
   magento-cloud snapshot:list
   ```

   The list returns information about the available snapshots:

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

1. Restore a snapshot using the snapshot ID from the list.

   ```bash
   magento-cloud snapshot:restore <snapshot-id>
   ```

## Roll back code

Backups and snapshots do _not_ include a copy of your code. Your code is already stored in the Git-based repository, so you can use Git-based commands to roll back (or revert) code. For example, use `git log --oneline` to scroll through previous commits; then use [`git revert`](https://git-scm.com/docs/git-revert) to restore code from a specific commit.

Also, you can choose to store code in an _inactive_ branch. Use git commands to create a branch instead of using `magento-cloud` commands. See about [Git commands](../dev-tools/cloud-cli-overview.md#git-commands) in the Cloud CLI topic.
