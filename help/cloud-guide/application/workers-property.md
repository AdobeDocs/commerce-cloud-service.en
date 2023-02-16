---
title: Workers
description: Learn how to configure the workers property in the Commerce application configuration file.
exl-id: d6816925-5912-45ca-8255-6c307e58542d
---
# Workers property

You can define zero or multiple work instances for each application. A worker instance runs as a container, independent from the web instance and without a running Nginx instance. Also, you do not need to set up a web server on the worker instance (using Node.js or Go) because the router cannot direct public requests to the worker.

A worker instance has the exact same code and compilation output as a web instance. The container image is built once and deployed multiple times if needed using the same `build` hook and `dependencies`. You can customize the container and allocated resources.

Use a worker instance when:

- Queue workers or updating indexes
- Tasks should happen "now", but not block a web request
- Tasks are large enough that they risk blocking a deploy, even if they are subdivided
- The task in question is a continually running process rather than a stream of discrete units of work

A basic, common worker configuration in the `.magento.app.yaml` file could look like the following:

```yaml
workers:
    queue:
        size: S
        commands:
            start: |
                php worker.php
```

This example defines a single worker named `queue`, with a small (size S) container, and runs the command `php worker.php` on startup. If `worker.php` exits, it is automatically restarted.

## Access the worker Container

You can connect to the worker instance to inspect logs and interact using SSH.

**To access a worker instance**:

1. On your local workstation, change to your project directory.
1. Use SSH to log in to the remote environment. Use the `worker` option to connect to a specific worker instance.

   ```bash
   magento-cloud ssh --worker=<worker-name>
   ```

   To connect to a worker called `queue` , such as in the earlier example, the SSH command looks similar to the following:

   ```terminal
   ssh projectID-master-7rqtwti--mymagento--queue@ssh.us.magentosite.cloud
   ```

## Commands and overrides

The `commands.start` key is required to launch commands with the worker application. You can use any valid shell command, although it is ideal to use the language of your application. If the command specified by the `start` key terminates, it restarts automatically.

>[!IMPORTANT]
>
>The `deploy` and `post_deploy` hooks and cron commands only run on the web container, not in worker instances.

## Inheritance

Definitions for `size`, `relationships`, `access`, `disk` and `mount`, and `variables` property are inherited by a worker, unless explicitly overridden. 

The following properties are the most commonly used to override [top-level settings](properties.md):

- `size`—allocate fewer resources to a container running only a single background process
- `variable`—instruct the application to run differently

## Multi-instance disk mounts

If you have multiple application instances defined (using both web and workers), each instance has independent disk mounts regardless of name or directive. Shared file storage between different application instances is not supported.

## Timing and Queueing

Though each worker queues behind another, the following configuration produces a consistent 2-second separation in time stamps in the `var/time.txt` file, regardless of the 8-second sleep within the PHP code:

```yaml
workers:
  time1:
    size: S
    commands:
      start: 'php -r "sleep(8); echo time() . PHP_EOL;" >> var/time.txt& sleep 2'
```
