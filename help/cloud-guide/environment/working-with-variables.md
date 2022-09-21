---
title: Working with variables
description: Learn about the different variables used in customizing build and deploy options Adobe Commerce on cloud infrastructure.
---

# Working with variables

Environment variables apply to a specific environment or branch. An environment _inherits_ variable definitions from the parent environment. You can override an inherited value by defining the variable specifically for the environment. For example, to set variables for development, define the variable values in the `.magento.env.yaml` file in the Integration environment. All environments branching from the Integration environment inherit those values. See [Deployment configuration](magento-env-yaml.md) for details about configuring your environment using the `.magento.env.yaml` file.

When using the CLI, you must set variables using one of the following methods:

- **Project-specific variables**—To set the same value for _all_ environments in your project, use the `magento-cloud project:variable:set` command. These variables are available at build and runtime in all environments.
- **Environment-specific variables**—To set a unique value for a _specific_ environment, use the `magento-cloud variable:set` command. These variables are available at runtime and are inherited by child environments. Specify the environment in your command using the `-e` option.

>[!NOTE]
>
>After setting project-specific variables, you must manually redeploy the remote environment for the change to take effect. Push the new commits to trigger a redeployment. Setting environment-specific variables in the Project Web Interface automatically redeploys the environment.

Use the following options to prevent a variable from being seen or inherited:

- `--inheritable false`—disables inheritance for child environments. This is useful for setting production-only values on the `master` branch and allowing all other environments to use a project-level variable of the same name.
- `--sensitive true`—marks the variable as _non-readable_ in the Project Web Interface. You cannot view the variable in the user interface; however, you can view the variable from the application container, like any other variable.

The following demonstrates a specific case for preventing a variable from being seen or inherited. You can only specify these options in the CLI. This case does not pertain to all available environment variables. 

```bash
magento-cloud variable:create --name <VARIABLE-NAME> --value <VARIABLE-VALUE> --inheritable false --sensitive true
```
