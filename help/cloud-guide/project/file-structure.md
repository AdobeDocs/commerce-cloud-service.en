---
title: Project structure
description: Learn about the file structure and project templates for Adobe Commerce on cloud infrastructure.
---

# Project structure

An Adobe Commerce on cloud infrastructure project includes essential files for credentials and application configuration. These files are available in as template according to the Adobe Commerce version. See the cloud templates based on Adobe Commerce version in the [`magento/magento-cloud` GitHub repository](https://github.com/magento/magento-cloud).

The following table describes the files included in a cloud project:

| File                      | Description  |
| ------------------------- | ------------ |
| `/.magento/routes.yaml`   | Configuration file that redirects `www` to the apex domain and `php` application to serve HTTP. See [Configure routes](../routes/routes-yaml.md). |
| `/.magento/services.yaml` | Configuration file that defines a MySQL instance (MariaDB), Redis, and OpenSearch or Elasticsearch. See [Configure services](../services/services-yaml.md). |
| `/app`                    | The `code` folder is used for custom modules. The `design` folder is used for [custom themes](../store/custom-theme.md). The `etc` folder contains configuration files for the application. |
| `/m2-hotfixes`            | Used for custom patches. |
| `/update`                 | A service folder used by the support module. |
| `.gitignore`              | Specify which files and directories to ignore. See [`.gitignore` reference](#ignoring-files). |
| `.magento.app.yaml`       | Configuration file that defines the properties to build your application. See [Configure application](../application/configure-app-yaml.md). |
| `.magento.env.yaml`       | Configuration file for the build, deploy, and post-deploy phases. The `ece-tools` package includes a sample of this file. See [Configure environments](../environment/configure-env-yaml.md). |
| `composer.json`           | Fetches Adobe Commerce and the configuration scripts to prepare your application. See [Required packages](../development/overview.md#required-packages). |
| `composer.lock`           | Stores version dependencies for every package. See [Required packages](../development/overview.md#required-packages). |
| `magento-vars.php`        | A file used to define [multiple stores](../store/multiple-sites.md) and sites using variables. |

{style="table-layout:auto"}

>[!NOTE]
>
>When you push your local changes to the remote server, the deploy script uses the values defined by configuration files in the `.magento` directory, then the script deletes the directory and its contents. Your local development environment is not affected.

## Application root directory

The location of the application root directory depends on the environment.

-  **Starter and Pro Integration**: `/app`
-  **Starter Production**: `/<project-ID>`
-  **Pro Staging**: `/<project-ID>_stg`
-  **Pro Production**: `/<project-ID>`

### Writable directories

The remote Integration, Staging, and Production environments are read only. The following directories are the *only* writable directories due to security reasons:

-  `var`
-  `pub/static`
-  `pub/media`
-  `app/etc`
-  `/tmp`

>[!NOTE]
>
>In Production and Staging environments, each node in the three-node cluster has a `/tmp` directory that is not shared with the other nodes.

## Ignoring files

We include a base `.gitignore` file with the Adobe Commerce on cloud infrastructure project repository. See the latest [.gitignore file in the magento-cloud repository](https://github.com/magento/magento-cloud/blob/master/.gitignore). If you need to add a file that is in the ignore list, you can use the `-f` (force) option when staging a commit:

```bash
git add <path/filename> -f
```

## Change base template

You can use the following steps to change the structure of an existing project to reflect the latest base template for Adobe Commerce on cloud infrastructure.

1. Clone project to local workstation.

1. Update the `composer.json` file with the following values for the `extra` section.

   ```json
   "extra": {
       "magento-force": true
       "magento-deploystrategy": "copy"
   }
   ```

1. Add the `.gitignore` file designed for the base template. For example, if you need the `.gitignore` file for the version 2.2.6 template, use the [.gitignore for 2.2.6](https://github.com/magento/magento-cloud/blob/2.2.6/.gitignore) file as a reference.

1. Clear the git cache.

   ```bash
   git rm -r --cached .
   ```

1. Add and commit changes.

   ```bash
   git add -A && git commit -m "Update base template"
   ```

{{redeploy-warning}}
