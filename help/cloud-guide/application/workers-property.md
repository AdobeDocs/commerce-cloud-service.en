---
title: Workers
description: Learn how to configure the workers property in the Commerce application configuration file.
exl-id: d6816925-5912-45ca-8255-6c307e58542d
---
# Workers property

You can define a worker to run independently from the web instance without a running Nginx instance. You do not need to set up a web server on the worker instance (using Node.js or Go) because the router cannot direct public requests to the worker. This makes the worker instance ideal for background tasks or continually running tasks that risk blocking a deployment.

## Configure a worker

Workers are available to use with Pro Staging and Production environments. Pro Integration and Starter environments can opt to use the [CRON_CONSUMERS_RUNNER](../environment/variables-deploy.md#cron_consumers_runner) variable.

To configure a worker in Pro Staging or Production, [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) and include the following information:

- Project ID
- Environment
- YAML configuration with start commands

You can configure one process per worker. A basic, common worker configuration in the `.magento.app.yaml` file could look like the following:

```yaml
workers:
    queue:
        size: S
        commands:
            start: |
                php ./bin/magento queue:consumers:start commerce.eventing.event.publish
```

This example defines a single worker named `queue`, with a small (size S) level of resource allocation, and runs the `php ./bin/magento` command on startup. The worker `queue` then runs on each node as a worker process. If the command exits, it is automatically restarted.

## Commands and overrides

The `commands.start` key is required to launch commands with the worker application. You can use any valid shell command, although it is ideal to use the language of your application. If the command specified by the `start` key terminates, it restarts automatically.

>[!IMPORTANT]
>
>The `deploy` and `post_deploy` hooks and cron commands only run on the web container, not in worker instances.

### Inheritance

Definitions for the `size`, `relationships`, `access`, `disk` and `mount`, and `variables` properties are inherited by a worker, unless explicitly overridden. 

The following properties are the most commonly used to override [top-level settings](properties.md):

- `size`—allocate fewer resources to a container running only a single background process
- `variable`—instruct the application to run differently

### Timing and queueing

Though each worker queues behind another, the following configuration produces a consistent two-second separation in time stamps in the `var/time.txt` file, regardless of the eight-second sleep within the PHP code:

```yaml
workers:
  time1:
    size: S
    commands:
      start: 'php -r "sleep(8); echo time() . PHP_EOL;" >> var/time.txt& sleep 2'
```
