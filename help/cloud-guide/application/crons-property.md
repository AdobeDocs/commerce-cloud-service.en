---
title: Crons property
description: See examples on how to configure the `crons` property in the Commerce application configuration file.
feature: Cloud, Configuration
exl-id: 67d592c1-2933-4cdf-b4f6-d73cd44b9f59
---
# Crons property

Adobe Commerce uses the `crons` property to schedule repetitive activities. It is ideal for scheduling a specific task to run at certain times of the day. Only one cron job can run at a time on the web instance for Adobe Commerce on cloud infrastructure projects because of the nature of read-only environments. It is a best practice to break down long-running tasks into smaller, queued tasks. Alternatively, you can build a [worker instance](workers-property.md).

Adobe recommends that you run `crons` as the [file system owner](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html). Do _not_ run `crons` as `root` or as the web server user.

This configuration is different from on-premises deployments of Adobe Commerce, which have multiple default cron jobs. See [Configure cron jobs](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html) in the _Configuration guide_.

## Set up cron jobs

The `crons` property describes processes that are triggered on a schedule. Each job requires a name and the following options:

- `spec`—The cron expression used for scheduling.
- `cmd`—The command to run on `start` and `stop`.
- `shutdown_timeout`—(_Optional_) If a cron job is canceled, this is the number of seconds after which a SIGKILL signal is sent to stop the job or process. The default is 10 seconds.
- `timeout`—(_Optional_) The maximum amount of time a cron job can run before timeout. Defaults to the maximum allowed value of 86400 seconds (24 hours).

By default, every Commerce cloud project has the following default `crons` configuration in the `.magento.app.yaml` file:

```yaml
crons:
    cronrun:
        spec: "* * * * *"
        cmd: "php bin/magento cron:run"
```

If your project requires custom cron jobs, you can add them to the default `crons` configuration. See [Build a cron job](#build-a-cron-job).

### `crontab`

Adobe Commerce added an auto-crons configuration option only to Pro projects to support self-service `crons` configuration on the Staging and Production environments. If this option is enabled, you can use `crontab` to review the cron configuration. This is _not_ available with Starter projects.

Although you can use `crontab` to review configuration on Pro projects, Adobe Commerce does not use `crontab` to run cron jobs for sites deployed on the cloud infrastructure.

**To review cron configuration on Pro environments**:

1. Use [SSH](../development/secure-connections.md#use-an-ssh-command) to log in to the remote environment.

1. List the scheduled cron processes.

   ```shell
   crontab -l
   ```

   >[!NOTE]
   >
   >If the `crontab -l` command returns a `Command not found` error, you must [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to enable the auto-crons self-service configuration option on your Pro project.

The following example shows the `crontab` output for an environment that has only the default `crons` configuration:

```terminal
username@hostname:~$ crontab -l
# Crontab is managed by the system, attempts to edit it directly will fail.
SHELL=/etc/platform/6fck2obu3244c/cron-run
MAILTO=""

# m h  dom mon dow  job_name

* * * * *           cronrun
```

## Build a cron job

A cron job includes the schedule and timing specification and the command to run at the scheduled time. For Starter environments and Pro Integration environments, the minimum interval is once per five minutes. For Pro Staging and Production environments, the minimum interval is once per minute. On Adobe Commerce on cloud infrastructure, you add custom cron jobs to the `.magento.app.yaml` file in the `crons` section. The general format is `spec` for scheduling and `cmd` to specify the command or custom script to run.

### Specification

Adobe Commerce uses a five-value expression for a `crons` specification (spec): `* * * * *`

1. Minute (0 through 59) For all Starter and Pro environments, the minimum frequency supported for cron jobs is five minutes. You may need to configure settings in your Admin.
2. Hour (0 through 23)
3. Day of month (1 through 31)
4. Month (1 through 12)
5. Day of week (0 through 6) (Sunday through Saturday; 7 is also Sunday on some systems)

Some examples:

- `00 */3 * * *` runs every three hours at the first minute (12:00 am, 3:00 am, 6:00 am)
- `20 */8 * * *` runs every 8 hours at minute 20 (12:20 am, 8:20 am, 4:20 pm)
- `00 00 * * *` runs once a day at midnight
- `00 * * * 1` runs once a week on Monday at midnight.

>[!NOTE]
>
>The `crons` time specified in the `.magento.app.yaml` file is based on the server timezone, not the timezone specified in the store configuration values in the database.

When determining the scheduling, consider the time it takes to complete the task. For example, if you run a job every three hours and the task takes 40 minutes to complete, you may consider changing the scheduled timing.

### Command

The `cmd` specifies the command or custom script to run. The command script format can include the following:

```text
<path-to-php-binary> <project-dir>/<script-command>
```

For example:

```yaml
crons:
    spec: "00 */8 * * *"
    cmd: "/usr/bin/php /app/abc123edf890/bin/magento export:start catalog_category_product"
```

In this example, `<path-to-php-binary>` is `/usr/bin/php`. The install directory, which includes the Project ID is `/app/abc123edf890/bin/magento`, and the script action is `export:start catalog_category_product`.

### Add custom cron jobs to your project

On the Adobe Commerce on cloud infrastructure platform, you can add customizations to the `crons` section of the [`.magento.app.yaml`](../application/configure-app-yaml.md) file.

>[!NOTE]
>
>For Starter environments and Pro Integration environments, the minimum interval is once per five minutes. For Pro Staging and Production environments, the minimum interval is once per minute. You cannot configure more frequent intervals than the default minimums.

On Adobe Commerce Pro projects, the [auto-crons feature](#set-up-cron-jobs) must be enabled on your project before you can add custom cron jobs to Staging and Production environments using the `.magento.app.yaml` file. If this feature is not enabled, [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to enable auto-crons.

**To add custom cron jobs**:

1. In your local development environment, edit the `.magento.app.yaml` file in the Adobe Commerce `/app` directory.

1. In the `crons` section, add your customization using the following format:

   ```yaml
   crons:
       <cron_name_1>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
       <cron_name_2>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
   ```

   In the following example, the `productcatalog` job exports the product catalog every eight hours, 20 minutes after the hour.

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

### Update cron jobs

To add, remove, or update a customized job, change the configuration in the `crons` section of the `.magento.app.yaml` file. Then, test the updates in the remote `integration` environment before pushing the changes to the Production and Staging environments.

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

Adobe has updated the Adobe Commerce on cloud infrastructure package to optimize cron processing on the Adobe Commerce on cloud infrastructure platform and to fix cron-related issues. If you encounter problems with cron processing, make sure that your project is using the most current version of the `ece-tools` package. See [Update ECE-Tools](../dev-tools/update-package.md).

You can review cron processing information in the application-level log files for each environment. See [Application logs](../test/log-locations.md#application-logs).

See the following Adobe Commerce Support articles for help with troubleshooting cron-related problems:

- [Cron tasks lock tasks from other groups](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.html)

- [Reset stuck cron jobs manually on the cloud](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/reset-stuck-magento-cron-jobs-manually-on-cloud.html)
