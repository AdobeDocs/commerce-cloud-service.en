---
title: Global Variables
description: See the list of environment variables that control actions in the Adobe Commerce on cloud infrastructure deployment process.
exl-id: 04c2861d-746d-42d4-a678-f6c7b464eb51
---
# Global variables

Global variables control actions across each phase of the Commerce deployment process: build, deploy, and post-deploy. Because global variables impact every phase, you must set them in the `global` stage of the `.magento.env.yaml` file:

```yaml
stage:
  global:
    GLOBAL_VARIABLE_NAME: value
```

For more information about customizing the build and deploy process:

- [Deployment configuration](configure-env-yaml.md)
- [Deployment process](../deploy/process.md)

## `ENABLE_EVENTING`

-  **Default**-_Not set_
-  **Version**—Adobe Commerce 2.4.5 and later

When set to `true`, enables cron to run message queue consumers. [Adobe I/O Events for Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/) uses message queues to expedite the delivery of critical events.

Adobe recommends that you also add the [`CRON_CONSUMERS_RUNNER`](./variables-deploy.md#cron_consumers_runner) variable to the `deploy` stage of the `.magento.env.yaml` file with `cron_run` set to `true`.

The following example shows a fully-configured `ENABLE_EVENTING` variable.

```yaml
stage:
  global:
    ENABLE_EVENTING: true
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 0
      consumers: []
```

## `MIN_LOGGING_LEVEL`

-  **Default**—_Not set_
-  **Version**—Adobe Commerce 2.1.4 and later

Overrides the minimum logging level for all output streams without changing the code. This helps when troubleshooting problems with deployment. For example, if your deployment fails, you can use this variable to increase the logging granularity globally. See [Log levels](log-handlers.md#log-levels). The `min_level` value in Logging handlers overwrites this setting.

```yaml
stage:
  global:
    MIN_LOGGING_LEVEL: debug
```

>[!WARNING]
>
>The setting for the `MIN_LOGGING_LEVEL` variable does not change the log level configuration for the file handler, which is set to `debug` by default.

## `SCD_ON_DEMAND`

-  **Default**—_Not set_
-  **Version**—Adobe Commerce 2.1.4 and later

Enable generation of static content when requested by a user (SCD). This is ideal for the development and testing workflow, because it decreases the deployment time.

Pre-loading the cache using the [`post_deploy` hook](../application/hooks-property.md) reduces site downtime. The cache warming is available only for Pro projects that contain Staging and Production environments in the Project Web Interface and for Starter projects. Add the `SCD_ON_DEMAND` environment variable to the `global` stage in the `.magento.env.yaml` file:

```yaml
stage:
  global:
    SCD_ON_DEMAND: true
```

The `SCD_ON_DEMAND` variable skips the SCD in both phases (build and deploy), clears the `pub/static` and `var/view_preprocessed` folders, and writes the following to the `app/etc/env.php` file:

```php?start_inline=1
return array(
   ...
   'static_content_on_demand_in_production' => 1,
   ...
);
```

## `SCD_MAX_EXECUTION_TIME`

-  **Default**—_Not set_
-  **Version**—Adobe Commerce 2.2.0 and later

Allows you to increase the maximum expected execution time for static content deployment.

By default, Adobe Commerce sets the maximum expected execution to 900 seconds, but in some scenarios you might need more time to complete the static content deployment for a Cloud project.

```yaml
stage:
  global:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

-  **Default**—_Not set_
-  **Version**—Adobe Commerce 2.4.2 and later

Set to `true` to prevent generating static content for parent themes during the build and deployment phases. When this option is set to `true`, less static content is generated, which improves your overall build and deployment times.

```yaml
stage:
  global:
    SCD_NO_PARENT: true
```

## `SCD_USE_BALER`

-  **Default**—_Not set_
-  **Version**—Adobe Commerce 2.3.0 and later

[Baler](https://github.com/magento/baler) is a module that scans your generated JavaScript code and creates an optimized JavaScript bundle. Deploying the optimized bundle to your site can reduce the number of network requests when loading your site and improve page load times.

Set to `true` to run Baler after performing static content deployment.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>You must install and configure the Baler module before using this feature. Because Baler is in alpha release, enable this option only on Staging environments.

## `SKIP_HTML_MINIFICATION`

-  **Default**:
   -  `true`—for `ece-tools` 2002.0.13 and later
   -  `false`—for earlier versions of `ece-tools`
-  **Version**—Adobe Commerce 2.1.4 and later

Enables or disables copying static view files to the `<magento_root>/init/` directory at the end of the build stage. If set to `true` files are not copied and HTML minification is available on request. Set this value to `true` to reduce downtime when deploying to Staging and Production environments.

-  **`false`**—Copies the `view_preprocessed` directory to the `<magento_root>/init/` directory at the end of the build phase, and restores the directory in the `<magento_root>/var` directory at the beginning of the deploy phase.
-  **`true`**—Enables on-demand HTML minification; does _not_ copy the `<magento_root>var/view_preprocessed` to the `<magento_root>/init/` directory at the end of the build phase.

Add the `SKIP_HTML_MINIFICATION` environment variable to the `global` stage in the `.magento.env.yaml` file:

```yaml
stage:
  global:
    SKIP_HTML_MINIFICATION: true
```

## `X_FRAME_CONFIGURATION`

-  **Default**—_Not set_
-  **Version**—Adobe Commerce 2.1.4 and later

Use the `X_FRAME_CONFIGURATION` variable to change the [`X-Frame-Options`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/security/xframe-options.html) header configuration for your Adobe Commerce site. This configuration controls how the browser renders a page in a `<frame>`, `<iframe>`, or `<object>`. Use one of the following options:

-  `DENY`—Page cannot be displayed in a frame.
-  `SAMEORIGIN`—(The default Adobe Commerce setting.) Page can be displayed only in a frame on the same origin as the page itself.

>[!WARNING]
>
>The `ALLOW-FROM <uri>` option has been deprecated because Adobe Commerce-supported browsers no longer support it. See [Browser compatibility](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility).

Add the `X_FRAME_CONFIGURATION` environment variable to the `global` stage in the `.magento.env.yaml` file:

```yaml
stage:
  global:
    X_FRAME_CONFIGURATION: SAMEORIGIN
```
