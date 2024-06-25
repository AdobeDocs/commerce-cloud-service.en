---
title: View and manage logs
description: Understand the types of log files available in the cloud infrastructure and where to find them.
last-substantial-update: 2023-05-23
exl-id: d7f63dab-23bf-4b95-b58c-3ef9b46979d4
---
# View and manage logs

Logs for Adobe Commerce on cloud infrastructure projects are useful for troubleshooting problems related to [build and deploy hooks](../application/hooks-property.md), cloud services, and the Adobe Commerce application.

You can view the logs from the file system, the [!DNL Cloud Console], and the `magento-cloud` CLI.

- **File system**—The `/var/log` system directory contains logs for all environments. The `var/log/` directory contains app-specific logs unique to a particular environment. These directories are not shared between nodes in a cluster. In Pro Production and Staging environments, you must check the logs on each node.

- **[!DNL Cloud Console]**—You can see build, deploy, and post-deploy log information in the environment _messages_ list.

- **Cloud CLI**—You can view local environment logs using the `magento-cloud log` command or remote environment logs using the `magento-cloud ssh` command.

## Log locations

System logs are stored in the following locations:

- Integration: `/var/log/<log-name>.log`
- Pro Staging: `/var/log/platform/<project-ID>_stg/<log-name>.log`
- Pro Production: `/var/log/platform/<project-ID>/<log-name>.log`

The value of `<project-ID>` depends on the project and whether the environment is Staging or Production. For example, with a project ID of `yw1unoukjcawe`, the Staging environment user is `yw1unoukjcawe_stg` and the Production environment user is `yw1unoukjcawe`.

Using that example, the deploy log is: `/var/log/platform/yw1unoukjcawe_stg/deploy.log`

### View remote environment logs

Most logs include events that occur in the remote environment. For Pro, there are multiple nodes and each node has unique logs. Use the following to see a list of all hosts:

```bash
magento-cloud ssh -p <project-ID> -e <environment-ID> --all
```

Sample response:

```terminal
1.ent-project-environment-id@ssh.region.magento.cloud
2.ent-project-environment-id@ssh.region.magento.cloud
3.ent-project-environment-id@ssh.region.magento.cloud
```

**To view a list of remote environment logs**:

```bash
magento-cloud ssh -e <environment-ID> "ls var/log"
```

Example for Pro:

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "ls var/log | grep error"
```

**To view a remote log**:

```bash
magento-cloud ssh -e <environment-ID> "cat var/log/cron.log"
```

Example for Pro:

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "cat var/log/cron.log"
```

>[!TIP]
>
>For Pro Staging and Pro Production environments, automatic log rotation, compression, and removal are enabled for log files with a fixed file name. Each log file type has a rotating pattern and lifetime.
>Full details of the environment's log rotation and lifespan of compressed logs can be found in: `/etc/logrotate.conf` and `/etc/logrotate.d/<various>`.
>For Pro Staging and Pro Production environments, you must [submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to ask for changes in the log rotation configuration.

>[!TIP]
>
>Log rotation cannot be configured in Pro Integration environments.
>For Pro Integration, you must implement a custom solution/script and [configure your cron](../application/crons-property.md) to run the script as needed.

>[!NOTE]
>
>Starter environments do not have log rotation.

## Build and Deploy logs

After pushing changes to your environment, you can review the logging from each hook in the `var/log/cloud.log` file. The log contains start and stop messages for each hook. In the following example, the messages are "`Starting post-deploy.`" and "`Post-deploy is complete.`"

Check the timestamps on log entries, verify, and locate the logs for a specific deployment. The following is a condensed example of log output that you can use for troubleshooting:

```terminal
Re-deploying environment project-integration-ID
  Executing post deploy hook for service `mymagento`
    [2019-01-03 19:44:11] NOTICE: Starting post-deploy.
    [2019-01-03 19:44:11] INFO: Validating configuration
    [2019-01-03 19:44:11] INFO: End of validation
    [2019-01-03 19:44:11] INFO: Enable cron
    [2019-01-03 19:44:11] INFO: Create backup of important files.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/env.php.bak for /app/app/etc/env.php was created.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/config.php.bak for /app/app/etc/config.php was created.
    [2019-01-03 19:44:11] INFO: php ./bin/magento cache:flush --ansi --no-interaction
    [2019-01-03 19:44:32] INFO: Warming up failed: http://integration-id-project.us.magentosite.cloud/
    [2019-01-03 19:44:32] NOTICE: Post-deploy is complete.
```

>[!TIP]
>
>When you configure your Cloud environment, you can set up [log-based Slack and email notifications](../environment/set-up-notifications.md) for build and deploy actions.

The following logs have a common location for all Cloud projects:

- **Deployment log**: `var/log/cloud.log`
- **Last deployment error log**: `var/log/cloud.error.log`
- **Debug log**: `var/log/debug.log`
- **Exception log**: `var/log/exception.log`
- **System log**: `var/log/system.log`
- **Support log**: `var/log/support_report.log`
- **Reports**: `var/report/`

Though the `cloud.log` file contains feedback from each stage of the deployment process, logs created by the deploy hook are unique to each environment. The environment-specific deploy log is in the following directories:

- **Starter and Pro integration**: `/var/log/deploy.log`
- **Pro Staging**: `/var/log/platform/<project-ID>_stg/deploy.log`
- **Pro Production**: `/var/log/platform/<project-ID>/deploy.log`

### Deploy log

The log for each deployment concatenates to the specific `deploy.log` file. The following example prints the deploy log of the current environment in the terminal:

```bash
magento-cloud log -e <environment-ID> deploy
```

Sample response:

```terminal
Reading log file projectID-branchname-ID--mymagento@ssh.zone.magento.cloud:/var/log/'deploy.log'

[2023-04-24 18:58:03.080678] Launching command 'b'php ./vendor/bin/ece-tools run scenario/deploy.xml\n''.

[2023-04-24T18:58:04.129888+00:00] INFO: Starting scenario(s): scenario/deploy.xml (magento/ece-tools version: 2002.1.14, magento/magento2-base version: 2.4.6)
[2023-04-24T18:58:04.364714+00:00] NOTICE: Starting pre-deploy.
...
```

{{scd-timing-warning}}

### Error log

Error and warning messages generated during the deployment process are written to both the `var/log/cloud.log` and the `var/log/cloud.error.log` files. The Cloud error log file contains only errors and warnings from the latest deployment. An empty file indicates a successful deployment with no errors.

You can view the log file using the [Cloud CLI SSH](#view-remote-environment-logs), or you can use ECE-Tools to show the errors with suggestions:

```bash
magento-cloud ssh -e <environment-ID> "./vendor/bin/ece-tools error:show"
```

Sample response:

```terminal
errorCode: 1001
stage: build
step: validate-config
suggestion: Please run the following commands:
1. bin/magento module:enable --all
2. git add -f app/etc/config.php
3. git commit -m 'Adding config.php'
4. git push
title: File app/etc/config.php does not exist
type: warning
---------------

errorCode: 1006
stage: build
step: validate-config
suggestion: Your application does not have the "post_deploy" hook enabled.
  In order to minimize downtime, add the following to ".magento.app.yaml":
  hooks:
      post_deploy: |
          php ./vendor/bin/ece-tools run scenario/post-deploy.xml
title: The configured state is not ideal
type: warning
```

Most error messages contain a description and suggested action. Use the [Error message reference for ECE-Tools](../dev-tools/error-reference.md) to look up the error code for further guidance. For further guidance, use the [Adobe Commerce deployment troubleshooter](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html).

## Application logs

Similar to deploy logs, application logs are unique for each environment:

| Log file            | Starter and Pro Integration | Description                                       |
| ------------------- | --------------------------- | ------------------------------------------------- |
| **Deploy log**      | `/var/log/deploy.log`       | Activity from the [deploy hook](../application/hooks-property.md). |
| **Post-deploy log** | `/var/log/post_deploy.log`  | Activity from the [post-deploy hook](../application/hooks-property.md). |
| **Cron log**        | `/var/log/cron.log`         | Output from cron jobs. |
| **Nginx access log**| `/var/log/access.log`       | On Nginx start, HTTP errors for missing directories and excluded file types. |
| **Nginx error log** | `/var/log/error.log`        | Startup messages useful for debugging configuration errors associated with Nginx. |
| **PHP access log**  | `/var/log/php.access.log`   | Requests to the PHP service. |
| **PHP FPM log**     | `/var/log/app.log`          | |

For Pro Staging and Production environments, the Deploy, Post-deploy, and Cron logs are available only on the first node in the cluster:

| Log file            | Pro Staging                                         | Pro Production                                  |
| ------------------- | --------------------------------------------------- | ----------------------------------------------- |
| **Deploy log**      | First node only:<br>`/var/log/platform/<project-ID>_stg/deploy.log` | First node only:<br>`/var/log/platform/<project-ID>/deploy.log` |
| **Post-deploy log** | First node only:<br>`/var/log/platform/<project-ID>_stg/post_deploy.log` | First node only:<br>`/var/log/platform/<project-ID>/post_deploy.log` |
| **Cron log**        | First node only:<br>`/var/log/platform/<project-ID>_stg/cron.log` | First node only:<br>`/var/log/platform/<project-ID>/cron.log` |
| **Nginx access log**| `/var/log/platform/<project-ID>_stg/access.log`     | `/var/log/platform/<project-ID>/access.log`     |
| **Nginx error log** | `/var/log/platform/<project-ID>_stg/error.log`      | `/var/log/platform/<project-ID>/error.log`      |
| **PHP access log**  | `/var/log/platform/<project-ID>_stg/php.access.log` | `/var/log/platform/<project-ID>/php.access.log` |
| **PHP FPM log**     | `/var/log/platform/<project-ID>_stg/php5-fpm.log`   | `/var/log/platform/<project-ID>/php5-fpm.log`   |

### Archived log files

The application logs are compressed and archived once per day and kept for one year. The compressed logs are named using a unique ID that corresponds to the `Number of Days Ago + 1`. For example, on Pro production environments a PHP access log for 21 days in the past is stored and named as follows:

```terminal
/var/log/platform/<project-ID>/php.access.log.22.gz
```

The archived log files are always stored in the directory where the original file was located before compression.

>[!NOTE]
>
>**Deploy** and **Post-deploy** log files are not rotated and archived. The entire deployment history is written within those log files.

## Service logs

Because each service runs in a separate container, the service logs are not available in the integration environment. Adobe Commerce on cloud infrastructure provides access to the web server container in the integration environment only. The following service log locations are for the Pro Production and Staging environments:

- **Redis log**: `/var/log/platform/<project-ID>_stg/redis-server-<project-ID>_stg.log`
- **Elasticsearch log**: `/var/log/elasticsearch/elasticsearch.log`
- **Java garbage collection log**: `/var/log/elasticsearch/gc.log`
- **Mail log**: `/var/log/mail.log`
- **MySQL error log**: `/var/log/mysql/mysql-error.log`
- **MySQL slow log**: `/var/log/mysql/mysql-slow.log`
- **RabbitMQ log**: `/var/log/rabbitmq/rabbit@host1.log`

Service logs are archived and saved for different periods of time, depending on the log type. For example, MySQL logs have the shortest lifetime—removed after seven days.

>[!TIP]
>
>Log file locations in the scaled architecture depend on the node type. See [Log locations in the Scaled architecture](../architecture/scaled-architecture.md#log-locations) topic.

## Log data for Pro Production and Staging

On Pro Production and Staging environments, use [New Relic log management](../monitor/log-management.md) integrated with your project to manage aggregated log data from all logs associated with your Adobe Commerce on cloud infrastructure project.

The New Relic Logs application provides a centralized log management dashboard to troubleshoot and monitor Adobe Commerce on cloud infrastructure Production and Staging environments. The dashboard also provides access to log data for Fastly CDN, Image Optimization, and Web application firewall (WAF) services. See [New Relic services](../monitor/new-relic-service.md).
