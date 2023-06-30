---
title: Build variables
description: See the list of environment variables that control actions in the Adobe Commerce on cloud infrastructure build phase.
feature: Cloud, Configuration, Build, SCD, Upgrade
recommendations: noDisplay, catalog
role: Developer
exl-id: 243aaa45-a5ef-4ed2-8800-3d0f07bf3740
---
# Build variables

The following _build_ variables control actions in the build phase and can inherit and override values from the [Global variables](variables-global.md). Insert these variables in the `build` stage of the `.magento.env.yaml` file:

```yaml
stage:
  build:
    BUILD_VARIABLE_NAME: value
```

For more information about customizing the build and deploy process:

- [Deployment configuration](configure-env-yaml.md)
- [Deployment process](../deploy/process.md)

The following variables were removed in v2.2:

-  `skip_di_clearing`
-  `skip_di_compilation`

## `ERROR_REPORT_DIR_NESTING_LEVEL`

-  **Default**—`1`
-  **Version**—Adobe Commerce 2.1.4 and later

Set the level of directory nesting for saving error report files to avoid filling the report directory with tens of thousands of files, which can make it difficult to manage and review the data. This setting defaults to `1`. Typically, you do not need to change the default value unless you have problems managing error report files in the `<magento_root>/var/report/` directory.

```yaml
stage:
  build:
    ERROR_REPORT_DIR_NESTING_LEVEL: 2
```

## `QUALITY_PATCHES`

-  **Default**—_Not set_
-  **Version**—Adobe Commerce 2.1.4 and later

Specify a list of Adobe Commerce quality patches to apply during deployment.

```yaml
stage:
  build:
    QUALITY_PATCHES: [ ]
```

The following example specifies three patches to apply during deployment.

```yaml
stage:
  build:
    QUALITY_PATCHES:
      - MC-31387
      - MDVA-4567
      - MC-456345
```

See [Apply patches](../development/apply-patches.md).

## `SCD_COMPRESSION_LEVEL`

-  **Default**—`6`
-  **Version**—Adobe Commerce 2.1.4 and later

Specifies which [gzip](https://www.gnu.org/software/gzip) compression level (`0` to `9`) to use when compressing static content; `0` disables compression.

```yaml
stage:
  build:
    SCD_COMPRESSION_LEVEL: 4
```

## `SCD_COMPRESSION_TIMEOUT`

-  **Default**—`600`
-  **Version**—Adobe Commerce 2.1.4 and later

When the time it takes to compress the static assets exceeds the compression timeout limit, it interrupts the deployment process. Set the maximum execution time, in seconds, for the static content compression command.

```yaml
stage:
  build:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_NO_PARENT`

-  **Default**—`false`
-  **Version**—Adobe Commerce 2.4.2 and later

Set to `true` to prevent generating static content for parent themes during the build phase.

Set `SCD_NO_PARENT: false` during the build phase so that generating static content for the parent themes does not impact site deployment or cause unnecessary site downtime. See [Static content deployment](../deploy/static-content.md).

```yaml
stage:
  build:
    SCD_NO_PARENT: false
```

## `SCD_MATRIX`

-  **Default**—_Not set_
-  **Version**—Adobe Commerce 2.1.4 and later

You can configure multiple locales per theme. This customization helps speed up the build process by reducing the number of unnecessary theme files. For example, you can build the _magento/backend_ theme in English and a custom theme in other languages.

The following example builds the `Magento/backend` theme with three locales:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

The following example builds three themes with three locales:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/blank":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/luma":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Or, you can choose to _not_ deploy a theme:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

-  **Default**—_Not set_
-  **Version**—Adobe Commerce 2.2.0 and later

Allows you to increase the maximum expected execution time for static content deployment.

By default, Adobe Commerce on cloud infrastructure sets the maximum expected execution to 900 seconds, but in some scenarios you might need more time to complete the static content deployment for a Cloud project.

```yaml
stage:
  build:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_STRATEGY`

-  **Default**—`quick`
-  **Version**—Adobe Commerce 2.2.0 and later

Customize the [deployment strategy](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) for static content. See [Deploy static view files](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Use these options _only_ if you have more than one locale:

-  `standard`—deploys all static view files for all packages.
-  `quick`—(_default_) minimizes deployment time.
-  `compact`—conserves disk space on the server. In Adobe Commerce version 2.2.4 and earlier, this setting overrides the value for `scd_threads` with a value of `1`.

```yaml
stage:
  build:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

-  **Default**—Automatic
-  **Version**—Adobe Commerce 2.1.4 and later

Sets the number of threads for static content deployment. The default value is set based on the detected CPU thread count and does not exceed a value of 4. Increasing the number of threads speeds up static content deployment; decreasing the number of threads slows it down. You can set the thread value, for example:

```yaml
stage:
  build:
    SCD_THREADS: 2
```

To further reduce deployment time, use [Configuration Management](../store/store-settings.md) with the `scd-dump` command to move static deployment into the build phase.

## `SCD_USE_BALER`

-  **Default**—_Not set_
-  **Version**—Adobe Commerce 2.3.0 and later

[Baler](https://github.com/magento/baler) scans your generated JavaScript code and creates an optimized JavaScript bundle. Deploying the optimized bundle to your site can reduce the number of network requests when loading your site and improve page load times.

Set to `true` to run Baler after performing static content deployment.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Because Baler is in alpha release, it is not advisable to use it in Production environments.

## `SKIP_COMPOSER_DUMP_AUTOLOAD`

-  **Default**— _Not set_
-  **Version**—Adobe Commerce 2.1.4 and later

Set to `true` to skip the `composer dump-autoload` command during a Cloud Docker installation. This variable is only relevant for Cloud Docker containers with writable file systems. In such cases, skipping the command prevents errors from other commands trying to access code from the deleted `generated` directory.

When Adobe Commerce runs `composer dump-autoload`, it creates autoload files with links to generated classes in the `generated` folder, which is not a problem in production environments with read-only files systems. However, for Cloud Docker installations with writable file systems (created only for testing and development using `./vendor/bin/ece-docker build:compose --with-test`), you can run the `bin/magento -n setup:upgrade` command without the `--keep-generated` option, which deletes the `generated` directory. If the directory is deleted, the `composer dump-autoload` command fails because the autoload contains links to files in the deleted directory.

```yaml
stage:
  build:
    SKIP_COMPOSER_DUMP_AUTOLOAD: true
```

## `SKIP_SCD`

-  **Default**— _Not set_
-  **Version**—Adobe Commerce 2.1.4 and later

Set to `true` to skip static content deployment during the build phase.

If you already deploy static content during the build phase with [Configuration Management](../store/store-settings.md), you can skip static content deployment for a quick build test.

On the build phase, set `SKIP_SCD: false` so that the static content build occurs during the build phase where the process does not impact site deployment or cause unnecessary site downtime. See [Static content deployment](../deploy/static-content.md).

```yaml
stage:
  build:
    SKIP_SCD: false
```

## `VERBOSE_COMMANDS`

-  **Default**—_Not set_
-  **Version**—Adobe Commerce 2.1.4 and later

Enable or disable the [Symfony](https://symfony.com/doc/current/console/verbosity.html) debug verbosity level for `bin/magento` CLI commands performed during the deployment phase.

>[!NOTE]
>
>To use VERBOSE_COMMANDS to control the detail in command output for both successful and failed `bin/magento` CLI commands, you must set [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

Choose the level of detail provided in the logs:

- `-v`= normal output
- `-vv`= more verbose output
- `-vvv` = verbose output ideal for debug

```yaml
stage:
  build:
    VERBOSE_COMMANDS: "-vv"
```
