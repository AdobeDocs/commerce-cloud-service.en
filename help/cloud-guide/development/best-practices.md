---
title: Best practices for upgrading your project
description: See a list of best practices for upgrading your project files.
exl-id: 7d0a2627-e4c5-46b4-9e6c-24d20fa4f92f
---
# Best practices for upgrading your project

Follow best practices for builds and deployment, and use the [Upgrades and patches](../development/commerce-version.md) workflow to upgrade your application. Use the following guidelines to plan your upgrade and post-upgrade work:

- **Backup your project**–Before upgrading the Adobe Commerce and any third-party or custom extensions, back up the database in Integration, Staging, and Production environments. See [Back up the database](../development/commerce-version.md#project-backup).

- **Check for compatibility issues**–

    - Ensure that any custom themes are compatible with the new Adobe Commerce version

    - After upgrading third party and custom extensions, use the `magento-cloud local:build` command to validate composer dependencies before deploying.

    - Review the Adobe Commerce release notes and extension documentation to ensure that you have implemented any workarounds or configuration changes required to address known functional issues and bugs related to the upgraded the Adobe Commerce version and extensions.

    - Ensure that the installed service versions are compatible with the new Adobe Commerce version, and upgrade services as needed. See [Services](../services/services-yaml.md).

    - Test your database to address any issues introduced by the updates to the Adobe Commerce version and extensions.

    - Make any required updates to environment-specific settings before deploying to the remote environment.

    - Ensure that the search service version is compatible with the PHP client version. See [Set up Elasticsearch](../services/elasticsearch.md) or [Set up OpenSearch](../services/opensearch.md).

- **Check database connectivity and available storage in remote environments**–

    - Use SSH to log in to the remote server and verify the connection to the MySQL database. See [Connect to the database](../services/mysql.md#connect-to-the-database).

    - Verify available storage in the remote environment–Use the `disk free` command to view and manage available disk space on your Cloud environments. See [Manage disk space](../storage/manage-disk-space.md).

        - Check the size of the upgraded database and verify that the `services.yaml` file has enough disk space allocated.

        - Free up disk space–Clear the cache, and clean the `/log` and `/tmp` directories before deploying.

- **Plan and perform a successful upgrade on local and Integration environments, before deploying to Staging**–After upgrade, test your deployment and resolve any issues.

- **Merge code to Staging, and then to Production**–Test and resolve any issues in the Staging environment before pushing changes to the Production environment.

- **Complete Post upgrade tasks**–

    - Use SSH to log in to the remote server and verify the following:

        - Check indexer status and reindex as needed. See [Manage the indexers](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html) in the _Configuration guide_.

        - Check the `cron` logs and the `cron_schedule` table in the Adobe Commerce database to verify cron status, and rerun cron jobs as needed.
      See [Logging](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html#logging) in the _Configuration Guide_.

    - Complete post-upgrade User Acceptance Testing UAT on Staging and Production environments and fix any issues related to third-party and custom extension upgrades.
