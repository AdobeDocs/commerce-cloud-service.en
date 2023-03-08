---
title: Snapshots and backup management
description: Learn how to manually back up and restore your Adobe Commerce on cloud infrastructure project.
exl-id: 1cb00db7-2375-4761-9c07-1e20a74859e0
---
# Snapshots and backup management

You can back up and restore Starter environments and Pro Integration environments at any time using a snapshot.

A _snapshot_ is a complete backup of an environment that includes all persistent data from all running services (for example, your MySQL database, Redis, and so on) and any files stored on the mounted volumes. Because an environment deploys as a read-only file system, restoring a snapshot is very fast.

The snapshot feature does **not** apply to the Pro Staging and Production environments. Snapshots for Starter and Pro Integration environments are different from Pro backup and disaster recovery backups. Snapshots are **not** automatic. It is _your_ responsibility to manually create a snapshot or set up a cron job to periodically take snapshots of your Starter or Pro Integration environments.

- If you want to roll back to previous code or remove added extensions in an environment, restoring a snapshot is not the recommended method. See [Rollbacks to remove code](#rollbacks-to-remove-code).
- If you must restore an unstable environment that does not have a snapshot, see [Restore an environment](../development/restore-environment.md).

## Create a snapshot

**To create a snapshot using the Project Web Interface**:

1. Log in to [the Project Web Interface](https://accounts.magento.cloud/user/).
1. In the left pane, click the name of the environment to back up.
1. In the top pane, click the **[!UICONTROL Snapshots]** icon. This is not available for a Pro Production or Staging environment.
1. Click **Create**.

**To create a snapshot using the `magento-cloud` CLI**:

1. On your local workstation, change to your project directory.
1. Check out the environment branch to snapshot.
1. Create the snapshot. For a full list of options, enter `magento-cloud snapshot:create --help`.

   ```bash
   magento-cloud snapshot:create
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

You have up to **seven days** to _restore_ a snapshot.

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

## Dump your database

You can create a copy of your database using the `ece-tools db-dump` command. By default, this command creates backups in the `/app/var/dump-main` directory for all database connections that are specified in the environment configuration. For example, if you configured your project to use split databases, the `db-dump` operation creates backups for each of the configured databases.

You can choose to back up selected databases by appending the database names to the command, for example:

```bash
php vendor/bin/ece-tools db-dump -- main sales
```

Consider the following guidelines:

- For Production environments, Adobe recommends completing database dump operations during off-peak hours to minimize service disruptions that occur when the site is in maintenance mode.
- The `db-dump` command creates an archive in your remote project directory called  `dump-<timestamp>.sql.gz`.
- If an error occurs during the dump operation, the command deletes the dump file to conserve disk space. Review the logs for details (`var/log/cloud.log`).
- For Pro Production environments, this command dumps only from one of three high-availability nodes, so production data written to a different node during the dump might not be copied. The command generates a `var/dbdump.lock` file to prevent the command from running on more than one node.

For help, use: `php vendor/bin/ece-tools db-dump --help`

**To create a database dump in the Staging or Production environment**:

1. [Use SSH to log in to the remote environment](../development/secure-connections.md#use-an-ssh-command) that contains the database to copy.

1. Create a backup of the database. To choose a target directory for the DB dump, use the `--dump-directory` option.

   ```bash
   php vendor/bin/ece-tools db-dump
   ```

   Sample response:

   ```terminal
   The db-dump operation switches the site to maintenance mode, stops all active cron jobs and consumer queue processes, and disables cron jobs before starting the dump process.
   Your site will not receive any traffic until the operation completes.
   Do you wish to proceed with this process? (y/N)? y
   2020-01-28 16:38:08] INFO: Starting backup.
   [2020-01-28 16:38:08] NOTICE: Enabling Maintenance mode
   [2020-01-28 16:38:10] INFO: Trying to kill running cron jobs and consumers processes
   [2020-01-28 16:38:10] INFO: Running Magento cron and consumers processes were not found.
   [2020-01-28 16:38:10] INFO: Waiting for lock on db dump.
   [2020-01-28 16:38:10] INFO: Start creation DB dump for main database...
   [2020-01-28 16:38:10] INFO: Finished DB dump for main database, it can be found here: /tmp/qxmtlseakof6y/dump-main-1580229490.sql.gz
   [2020-01-28 16:38:10] INFO: Backup completed.
   [2020-01-28 16:38:11] NOTICE: Maintenance mode is disabled.
   ```

>[!TIP]
>
>If you want to push this data into an environment, see [Migrate data and static files](../deploy/staging-production.md#migrate-static-files).

## Rollbacks to remove code

Adobe recommends creating a snapshot of the environment and a backup of the database before deployments.

If you must restore a snapshot specifically to remove new code and added extensions, the process can be complicated depending on the number of changes and when you roll back. Some rollbacks might require database changes.

Specifically for code, you should investigate reverting code changes from your branch before redeploying. If not, every deploy pushes the `master` branch (code and extensions) to the target environment again. See the [Deployment Process](../deploy/process.md).
