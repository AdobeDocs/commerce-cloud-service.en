---
title: Crons property
description: See examples on how to configure the `crons` property in the Commerce application configuration file.
---

# Crons property

Adobe Commerce uses cron jobs for numerous features to schedule activities. We recommend you run `cron` as the [file system owner](https://devdocs.magento.com/cloud/before/before-workspace-file-sys-owner.html). Do _not_ run cron as `root` or as the web server user.

The `crons` property describes processes that are triggered on a schedule and uses the following:

-  `spec`—The cron specification. For Starter environments and Pro Integration environments, the minimum interval is once per five minutes and once per one minute in Pro Staging and Production environments. You must complete [additional configurations](https://devdocs.magento.com/cloud/configure/setup-cron-jobs.html#add-cron) for cron configuration in those environments.
-  `cmd`—The command to execute.

A cron job is well suited for the following tasks:

-  They need to happen on a fixed schedule, not continually.
-  The task itself is not especially long, as a running cron job blocks a new deployment.
-  Or it is long, but can be easily divided into many small queued tasks.
-  A delay between when a task is registered and when it actually happens is acceptable.

By default, every Cloud project has the following default crons configuration to run the default cron jobs:

```yaml
crons:
    cronrun:
        spec: "* * * * *"
        cmd: "php bin/magento cron:run"
```

For Adobe Commerce 2.1.x, you can use only [workers](workers-property.md) and cron jobs. For Adobe Commerce 2.2.x, cron jobs launch consumers to process batches of messages, and do not require additional configuration.

## Set up cron jobs

We use only one cron for Adobe Commerce on cloud infrastructure projects because of the nature of read-only environments. This configuration is different from Adobe Commerce, which has three default cron jobs. See [Configure cron jobs](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html) in the Adobe Commerce documentation.

If your project requires custom cron jobs, you can add them to the default cron configuration.

**To verify cron configuration**:

1. On your local workstation, change to your project directory.

1. Review the cron configuration in the `crons` section of the [.magento.app.yaml](../application/crons-property.md) configuration file.

### crontab

Adobe Commerce added an auto-crons configuration option to all Pro projects to support self-service cron configuration on Staging and Production environments using the `.magento.app.yaml` file. If this option is enabled, you can use `crontab` to review the cron configuration.

Although you can use crontab to review configuration on Pro plan projects, Adobe Commerce does not use crontab to run cron jobs for sites deployed on our cloud infrastructure.

**To review cron configuration on Pro environments**:

1. Use [SSH](../development/secure-connections.md#use-an-ssh-command) to log in to the remote environment.

1. List the scheduled cron processes.

   ```shell
   crontab -l
   ```

   >[!NOTE]
   >
   >If the `crontab -l` command returns a `Command not found` error, you must submit a [Support ticket](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) to enable the auto-crons self-service configuration option on your Adobe Commerce on cloud infrastructure project.

The following example shows the crontab output for an environment that has only the default `crons` configuration:

```terminal
username@hostname:~$ crontab -l
# Crontab is managed by the system, attempts to edit it directly will fail.
SHELL=/etc/platform/6fck2obu3244c/cron-run
MAILTO=""

# m h  dom mon dow  job_name

* * * * *           cronrun
```

## Build a cron job

A cron job includes the schedule and timing specification and the command to run at the scheduled time. For example, the general format is:

```terminal
* * * * * <command>
```

Adobe Commerce uses a five value specification for a cron job: `* * * * *`

1. Minute (0 through 59) For all Starter and Pro environments, the minimum frequency supported for cron jobs is five minutes. You may need to configure settings in your Admin.
2. Hour (0 through 23)
3. Day of month (1 through 31)
4. Month (1 through 12)
5. Day of week (0 through 6) (Sunday through Saturday; 7 is also Sunday on some systems)

Some examples:

- `00 */3 * * *` runs every three hours at the first minute (12:00 am, 3:00 am, 6:00 am, and so on)
- `20 */8 * * *` runs every 8 hours at minute 20 (12:20 am, 8:20 am, 4:20 pm, and so on)
- `00 00 * * *` runs once a day at midnight
- `00 * * * 1` runs once a week on Monday at midnight.

>[!NOTE]
>
>The cron time specified in the `.magento.app.yaml` file is based on the server timezone, not the timezone specified in the store configuration values in the database.

When determining the scheduling of custom cron jobs, consider the time it takes to complete the task. For example, if you run a job every three hours and the task takes 40 minutes to complete, you may consider changing the scheduled timing.

On Adobe Commerce on cloud infrastructure, you add custom cron job configuration to the `.magento.app.yaml` file in the `crons` section. The general format is `spec` for scheduling and `cmd` to specify the command or custom script to run.

For the command script, the format includes:

```text
<path-to-php-binary> <project-dir>/<script-command>
```

The following is an example cron job:

```yaml
crons:
    spec: "00 */8 * * *"
    cmd: "/usr/bin/php /app/abc123edf890/bin/magento export:start catalog_category_product"
```

In this example, `<path-to-php-binary>` is `/usr/bin/php`. The install directory, which includes the Project ID is `/app/abc123edf890/bin/magento`, and the script action is `export:start catalog_category_product`.

## Add custom cron jobs to your project

On the Adobe Commerce on cloud infrastructure platform, you configure custom cron jobs by adding them to the [`.magento.app.yaml`](../application/configure-app-yaml.md) file in the `crons` section.

>[!NOTE]
>
>The default cron interval for all environments is one minute. The default cron interval in all other regions is five minutes for Pro Integration environments and one minute for Pro Staging and Production environments. You cannot configure more frequent intervals than the default minimums.

On Adobe Commerce Pro projects, the [auto-crons feature](#set-up-cron-jobs) must be enabled on your Adobe Commerce on cloud infrastructure project before you can add custom cron jobs to Staging and Production environments using `.magento.app.yaml`. If this feature is not enabled, submit a [Support ticket](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) to enable auto-crons.

**To add custom cron jobs**:

1. In your local development environment, edit the `.magento.app.yaml` file in the Adobe Commerce `/app` directory.

1. In the `crons` section, add your custom cron code in the following format:

   ```yaml
   crons:
       <cron_name_1>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
       <cron_name_2>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
   ```

   For example, you can add a custom cron job to export the product catalog and configure it to run every eight hours, 20 minutes after the hour.

   ```yaml
   crons:
       magento:
           spec: '* * * * *'
           cmd: 'php bin/magento cron:run'
       productcatalog:
           spec: '20 */8 * * *'
           cmd: 'bin/magento export:start catalog_product_category'
   ```

1. Add, commit, and push code changes.

   ```bash
   git add .magento.app.yaml && git commit -m "cron config updates" && git push origin <branch-name>
   ```

## Update custom cron jobs

To add, remove, or update a custom cron job, change the configuration in the `crons` section of the `.magento.app.yaml` file for the Integration environment. Then, test the updates in the Integration environment before pushing the changes to the Production and Staging environments.

## Disable cron jobs

You can manually disable cron jobs before you complete maintenance tasks like reindexing or cleaning the cache to prevent performance issues. You can use the `ece-tools` CLI command `cron:disable` to disable all cron jobs and stop any active cron processes.

**To disable cron jobs**:

1. On your local workstation, change to your project directory.

1. Use SSH to log in to the remote environment.

   ```bash
   magento-cloud ssh
   ```

1. Disable cron jobs and stop active cron processes.

   ```shell
   ./vendor/bin/ece-tools cron:disable
   ```

1. After you complete any required maintenance tasks, ensure that you enable the cron jobs again.

   ```shell
   ./vendor/bin/ece-tools cron:enable
   ```

## Troubleshooting cron jobs

Adobe has updated the Adobe Commerce on cloud infrastructure package to optimize cron processing on the Adobe Commerce on cloud infrastructure platform and to fix cron-related issues. If you encounter problems with cron processing, make sure that your project is using the most current version of the `ece-tools` package. See [Upgrades and patches](https://devdocs.magento.com/cloud/project/project-upgrade-parent.html).

You can review cron processing information in the application-level log files for each environment. See [Application logs](../monitor/log-locations.md#application-logs).

See the following Adobe Commerce Support articles for help with troubleshooting cron-related problems:

-  [Cron tasks lock tasks from other groups](https://support.magento.com/hc/en-us/articles/360029219812-Cron-tasks-lock-tasks-from-other-groups)

-  [Reset stuck cron jobs manually on the cloud](https://support.magento.com/hc/en-us/articles/360000097713-Reset-stuck-Magento-cron-jobs-manually-on-Cloud)
