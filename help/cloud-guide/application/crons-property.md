---
title: Crons property
description: See examples on how to configure the `crons` property in the Commerce application configuration file.
---

# Crons property

Describes processes that are triggered on a schedule. We recommend you run `cron` as the [file system owner](https://devdocs.magento.com/cloud/before/before-workspace-file-sys-owner.html). Do _not_ run cron as `root` or as the web server user.

The `crons` property supports the following:

-  `spec`—The cron specification. For Starter environments and Pro Integration environments, the minimum interval is once per five minutes and once per one minute in Pro Staging and Production environments. You must complete [additional configurations](https://devdocs.magento.com/cloud/configure/setup-cron-jobs.html#add-cron) for cron configuration in those environments.
-  `cmd`—The command to execute.

A cron job is well suited for the following tasks:

-  They need to happen on a fixed schedule, not continually.
-  The task itself is not especially long, as a running cron job will block a new deployment.
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

If your project requires custom cron jobs, you can add them to the default cron configuration. See [Set up cron jobs](https://devdocs.magento.com/cloud/configure/setup-cron-jobs.html).
