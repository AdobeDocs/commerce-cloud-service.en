---
title: Properties
description: Use the property list as a reference when configurion the Commerce application for build and deploy to the cloud infrastructure.
---

# Properties for application configuration

The `.magento.app.yaml` file uses properties to manage environment support for the Commerce application. 

| Name   | Description                       | Default | Required |
| ------ | --------------------------------- | ------- | -------- |
| [`access`](#access) | Customize user roles | — | No |
| [`crons`](crons-property.md) | Update specs and schedule cron jobs | — | No |
| [`dependencies`](#dependencies) | Enable additional dependencies | `php:composer/composer: '2.2.4'` | No |
| [`disk`](#disk) | Define the persistent disk size | `5120` | Yes |
| [`firewall`](firewall-property.md) | (Starter only) Control outbound traffic | — | No |
| [`hooks`](hooks-property.md) | Customize shell commands for the build, deploy, and post-deploy phases | — | No |
| [`mounts`](#mounts) | Set paths | `"var": "shared:files/var"`<br>`"app/etc": "shared:files/etc"`<br>`"pub/media": "shared:files/media"`<br>`"pub/static": "shared:files/static"` | No |
| [`name`](#name) | Define the application name | `mymagento` | Yes |
| [`relationships`](#relationships) | Map services | `database: "mysql:mysql"`<br>`redis: "redis:redis"`<br>`opensearch: "opensearch:opensearch"` | No |
| [`type`](#type-and-build) | Set the base container image | `php:8.1` | Yes |
| [`variables`](variables-property.md) | Apply an environment variable for a specific Commerce version | — | No |
| [`web`](web-property.md) | Handle external requests | — | Yes |
| [`workers`](workers-property.md) | Handle external requests | — | Yes, if not using web |

>[!NOTE]
>
>For Pro Staging and Production environments, you must [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to update the `mounts` and `disk` configuration for your application. When you submit the ticket, indicate the required configuration changes and include an updated version of your `.magento.app.yaml` file.

## `name`

The `name` property provides the application name used in the [`routes.yaml`](../routes/routes-yaml.md) file to define the HTTP upstream (by default, `mymagento:http`). For example, if the value of `name` is `app`, you must use `app:http` in the upstream field.

>[!WARNING]
>
>Do not change the name of the application after it has been deployed. Doing so will result in data loss.

## `type` and `build`

The `type`  and `build` properties provide information about the base container image to build and run the project.

The supported `type` language is PHP. Specify the PHP version as follows:

```yaml
type: php:<version>
```

The `build` property determines what happens by default when building the project. The `flavor` specifies a default set of build tasks to run. The following example shows the default configuration for `type` and `build` from `magento-cloud/.magento.app.yaml`:

```yaml
# The toolstack used to build the application.
type: php:8.1
build:
    flavor: none

dependencies:
    php:
        composer/composer: '2.2.4'
```

### Installing and using Composer 2

The `build: flavor:` property is not used for Composer 2.x; therefore, you must manually install Composer during the build phase. To install and use Composer 2.x in your Starter and Pro projects, you need to make three changes to your `.magento.app.yaml` configuration:

1. Remove `composer` as the `build: flavor:` and add `none`. This change prevents Cloud from using the default 1.x version of Composer to run build tasks.
1. Add `composer/composer: '^2.0'` as a `php` dependency to install Composer 2.x.
1. Add the `composer` build tasks to a `build` hook to run the build tasks using Composer 2.x.

Use the following configuration fragments in your own `.magento.app.yaml` configuration:

```yaml
# 1. Change flavor to none.
build:
    flavor: none

# 2. Add composer ^2.0 as a php dependency.
dependencies:
    php:
        composer/composer: '^2.0'

# 3. Add a build hook to run the build tasks using Composer 2.x.
hooks:
    build: |
        set -e
        composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
```

## `dependencies`

Enables you to specify dependencies that your application might need during the build process.

Adobe Commerce supports dependencies on the following languages:

-  PHP
-  Ruby
-  Node.js

Those dependencies are independent of the eventual dependencies of your application, and are available in the `PATH`, during the build process and in the runtime environment of your application.

You can specify those dependencies as follows:

```yaml
ruby:
   sass: "~3.4"
nodejs:
   grunt-cli: "~0.3"
```

## `disk`

Defines the persistent disk size of the application in MB.

```yaml
disk: 5120
```

The minimal recommended disk size is 256MB. If you see the error `UserError: Error building the project: Disk size may not be smaller than 128MB`, increase the size to 256MB.

## `relationships`

Defines the service mapping in the application.

The relationship `name` is available to the application in the `MAGENTO_CLOUD_RELATIONSHIPS` environment variable. The `<service-name>:<endpoint-name>` relationship maps to the name and type values defined in the `.magento/services.yaml` file.

```yaml
relationships:
    <name>: "<service-name>:<endpoint-name>"
```

The following is an example of the default relationships:

```yaml
relationships:
    database: "mysql:mysql"
    redis: "redis:redis"
    opensearch: "opensearch:opensearch"
    rabbitmq: "rabbitmq:rabbitmq"
```

See [Services](../services/services-yaml.md) for a full list of currently supported service types and endpoints.

## `mounts`

An object whose keys are paths relative to the root of the application. The mount is a writable area on the disk for files. The following is a default list of mounts configured in the `magento.app.yaml` file using the `volume_id[/subpath]` syntax:

```yaml
 # The mounts that will be performed when the package is deployed.
mounts:
    "var": "shared:files/var"
    "app/etc": "shared:files/etc"
    "pub/media": "shared:files/media"
    "pub/static": "shared:files/static"
```

The format for adding your mount to this list is as follows:

```bash
"/public/sites/default/files": "shared:files/files"
```

-  `shared`—Shares a volume between your applications inside an environment.
-  `disk`—Defines the size available for the shared volume.

You can make the mount web accessible by adding it to the [`web`](web-property.md) block of locations.

>[!WARNING]
>
>Once your site has data, do not change the `subpath` portion of the mount name. This value is the unique identifier for the files area. If you change this name, you will lose all site data stored at the old location.

## `access`

The `access` property indicates a minimum user role level that is allowed SSH access to the environments. The available user roles are:

-  `admin`—Can change settings and execute actions in the environment. Also has _contributor_ and _viewer_ rights.
-  `contributor`—Can push code to this environment and branch from the environment. Also has _viewer_ rights.
-  `viewer`—Can view the environment only.

The default user role is `contributor`, which restricts the SSH access from users with only _viewer_ rights. You can change the user role to `viewer` to allow SSH access for users with only _viewer_ rights:

```yaml
access:
    ssh: viewer
```
