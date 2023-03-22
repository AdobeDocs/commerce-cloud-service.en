---
title: Back up the database
description: Learn how to create a database dump for an Adobe Commerce on cloud infrastructure project.
---

# Back up the database

You can create a copy of your database using the `ece-tools db-dump` command without capturing the whole of environment data from services and mounts. By default, this command creates backups in the `/app/var/dump-main` directory for all database connections that are specified in the environment configuration. The DB dump operation switches the application to maintenance mode, stops consumer queue processes, and disables cron jobs before the dump begins.

>[!TIP]
>
>If you configured your project to use [split databases](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/storage/split-db/multi-master.html), the `db-dump` operation creates backups for each of the configured databases. Use the `php vendor/bin/ece-tools wizard:split-db-state` command to verify.

You can choose to back up multiple databases by appending the database names to the command. The following example backs up two databases: `main` and `sales`:

```bash
php vendor/bin/ece-tools db-dump -- main sales
```

Consider the following guidelines for db-dump:

- For Production environments, Adobe recommends completing database dump operations during off-peak hours to minimize service disruptions that occur when the site is in maintenance mode.
- If an error occurs during the dump operation, the command deletes the dump file to conserve disk space. Review the logs for details (`var/log/cloud.log`).
- For Pro Production environments, this command dumps only from _one_ of the three high-availability nodes, so production data written to a different node during the dump might not be copied. The command generates a `var/dbdump.lock` file to prevent the command from running on more than one node.
- For a backup of all environment services, Adobe recommends creating a [snapshot](snapshots.md).

Use the `php vendor/bin/ece-tools db-dump --help` command for more options.

**To create a database dump in the Staging or Production environment**:

1. [Use SSH to log in to the remote environment](../development/secure-connections.md#use-an-ssh-command) that contains the database to copy.

1. List the environment relationships to find the database login information.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   or

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

1. Create a backup of the database. To choose a target directory for the DB dump, use the `--dump-directory` option.

   ```bash
   php vendor/bin/ece-tools db-dump -- main
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

1. The `db-dump` command creates an archive in your remote project directory called  `dump-<timestamp>.sql.gz`.

>[!TIP]
>
>If you want to push this data to a specific environment, see [Migrate data and static files](../deploy/staging-production.md#migrate-static-files).
