---
title: Snapshots and backup management
description: Learn how to manually back up and restore your Adobe Commerce on cloud infrastructure project.
exl-id: 1cb00db7-2375-4761-9c07-1e20a74859e0
---
# Snapshots and backup management

You can perform a manual backup of active Starter and Pro Integration environments at any time using the **[!UICONTROL Snapshots]** button in the Project Web Interface or using the `magento-cloud snapshot:create` command.

A _snapshot_ is a complete backup of environment data that includes all persistent data from running services (Redis session, MySQL database) and any files stored on the mounted volumes (var, pub/media, app/etc). The backup does _not_ include code, since the code is already stored in the Git repository. You cannot download a copy of a snapshot. The snapshots feature does **not** apply to the Pro Staging and Production environments.

Unlike the [automatic live backups for Pro Production environments](../architecture/pro-architecture.md#backup-and-disaster-recovery), snapshots are **not** automatic. It is _your_ responsibility to manually create a snapshot or set up a cron job to periodically take snapshots of your Starter or Pro Integration environments.

## Create a snapshot

You must have an [Admin role](../project/user-access.md) for the environment.

**To create a snapshot using the Project Web Interface**:

1. Log in to [the Project Web Interface](https://accounts.magento.cloud/user/).
1. In the left pane, click the name of the environment to back up.
1. In the top pane, click the **[!UICONTROL Snapshots]** icon. This option is not available for a Pro Production or Staging environment.
1. Click **Create**.

**To create a snapshot using the `magento-cloud` CLI**:

1. On your local workstation, change to your project directory.
1. Check out the environment branch to snapshot.
1. Create the snapshot. The `--live` option leaves the environment running to avoid downtime. For a full list of options, enter `magento-cloud snapshot:create --help`.

   ```bash
   magento-cloud snapshot:create --live
   ```

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

## Restore a snapshot

You must have an [Admin role](../project/user-access.md) for the environment. You have up to **seven days** to _restore_ a snapshot. Restoring a snapshot does not change the code of the current git branch.

Restoration times may vary depending on the size of your database:

- large database (200+ GB) can take 5 hours
- medium database (150 GB) can take 2 1/2 hours
- small database (60 GB) can take 1 hour

>[!TIP]
>
>Restoring without a snapshot:
>
>- To roll back to previous code or remove added extensions in an environment. See [Roll back code](#roll-back-code).
>- To restore an unstable environment that does _not_ have a snapshot, see [Restore an environment](../development/restore-environment.md).

**To restore a snapshot using the Project Web Interface**:

1. Log in to [the Project Web Interface](https://accounts.magento.cloud/user/).
1. In the left pane, click the name of the environment to restore.
1. In the environment messages, select **snapshot** from the _all types of_ drop-down list.
1. Click **restore** next to the snapshot.
1. Review the Snapshot restore date and click **Restore**.

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

Snapshots do _not_ include a copy of your code. Your code is already stored in the Git-based repository, so you can use Git-based commands to roll back (or revert) code. For example, use `git log --oneline` to scroll through previous commits; then use [`git revert`](https://git-scm.com/docs/git-revert) to restore code from a specific commit.

Also, you can choose to store code in an _inactive_ branch. Use git commands to create a branch instead of using `magento-cloud` commands. See about [Git commands](../dev-tools/cloud-cli.md#git-commands) in the Cloud CLI topic.
