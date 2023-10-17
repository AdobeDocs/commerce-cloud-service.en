---
title: Variable levels and options
description: Learn about the different variable levels and options used in customizing your Adobe Commerce on cloud infrastructure project runtime environment.
feature: Cloud, Configuration, Security
exl-id: 11aa0862-94c0-47fb-946a-0148f75cc24c
---
# Variable levels

Project variables apply to all environments within the project. Environment variables apply to a specific environment or branch. An environment _inherits_ variable definitions from the parent environment. You can override an inherited value by defining the variable specifically for the environment. For example, to set variables for development, define the variable values in the `.magento.env.yaml` file in the Integration environment. All environments branching from the Integration environment inherit those values. See [Deployment configuration](configure-env-yaml.md) for details about configuring your environment using the `.magento.env.yaml` file.

To set variables using the CLI, first choose one of the following levels:

- **Project-specific variables**—To set the same value for _all_ environments in your project. These variables are available at build and runtime in all environments.

    ```bash
    magento-cloud variable:create --level project --name <variable-name> --value <variable-value>
    ```

- **Environment-specific variables**—To set a unique value for a _specific_ environment. These variables are available at runtime and are inherited by child environments. Specify the environment in your command using the `-e` option.

    ```bash
    magento-cloud variable:create --level environment --name <variable-name> --value <variable-value>
    ```

>[!NOTE]
>
>After setting project-specific variables, you must manually redeploy the remote environment for the change to take effect. Push the new commits to trigger a redeployment. Setting environment-specific variables in the Project Web Interface automatically redeploys the environment.

## Visibility

You can limit the visibility of a variable during build or runtime using the `--visible-<build|runtime>` command. Also, there are options to set inheritance and sensitivity.

Use the following options to prevent a variable from being seen or inherited:

- `--inheritable false`—disables inheritance for child environments. This is useful for setting production-only values on the `master` branch and allowing all other environments to use a project-level variable of the same name.
- `--sensitive true`—marks the variable as _non-readable_ in the Project Web Interface. You cannot view the variable in the user interface; however, you can view the variable from the application container, like any other variable.

The following demonstrates a specific case for preventing a variable from being seen or inherited. You can only specify these options in the CLI. This case does not pertain to all available environment variables.

```bash
magento-cloud variable:create --name <variable-name> --value <variable-value> --inheritable false --sensitive true
```

## Verify variable levels and values

You can view a list of existing variables:

```bash
magento-cloud variables
```

```terminal
Variables on the project Project-Name (<project-id>), environment <environment-name>:
+----------------------------+-------------+-------------------------------------------+
| Name                       | Level       | Value                                     |
+----------------------------+-------------+-------------------------------------------+
| env:COMPOSER_AUTH          | project     | {                                         |
|                            |             |    "http-basic": {                        |
|                            |             |       "repo.magento.com": {               |
|                            |             |       "username":                         |
|                            |             | "<public-key>",                           |
|                            |             |       "password":                         |
|                            |             | "<private-key>"                           |
|                            |             |     }                                     |
|                            |             |   }                                       |
|                            |             | }                                         |
| ADMIN_EMAIL                | project     | admin@123.com                             |
| ADMIN_EMAIL                | environment | admin@123.com                             |
| ADMIN_PASSWORD             | environment | password                                  |
| ADMIN_URL                  | environment | admin123                                  |
| ADMIN_USERNAME             | environment | admin                                     |
| php:newrelic.license       | environment | xxxx71fb030366182117f955a22e4baf8exxxxxx  |
+----------------------------+-------------+-------------------------------------------+
```
