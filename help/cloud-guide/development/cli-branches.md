---
title: Manage branches with the CLI
description: Learn how to manage the environment branches for Adobe Commerce on cloud infrastructure using the Cloud CLI.
role: Developer
feature: Cloud, Install
exl-id: a871c7e2-4506-4a05-8fc2-fc5ef2afe609
---
# Manage branches with the CLI

To install the `magento-cloud` CLI, see the [Cloud CLI reference](../dev-tools/cloud-cli-overview.md). After you install the `magento-cloud` CLI and set up SSH keys for remote access to your cloud infrastructure, you can use `magento-cloud` CLI commands to manage the environments for your projects. For information about the environment architecture, see [Starter architecture](../architecture/starter-architecture.md) or [Pro architecture](../architecture/pro-architecture.md).

To manage the branches and environments with the Project Web Interface, see [Manage branches with the Project Web Interface](../project/console-branches.md).

## Use CLI commands

The `magento-cloud` CLI commands are similar to Git commands. You can use them to connect to your project and manage your environments. Although you can run the commands from any directory, we recommend that you run them from a project directory. When run from a project directory, you can omit the `-p <project-ID>` parameter. See the [Cloud CLI reference](../dev-tools/cloud-cli-overview.md).

## Clone the project

The following instructions use a combination of `magento-cloud` CLI commands and Git commands to clone your project to your local workstation. To see a full list of `magento-cloud` CLI commands, use the `magento-cloud list` command.

>[!IMPORTANT]
>
>Some Git commands cannot complete an action in your Adobe Commerce on cloud infrastructure project. For example, you can create a branch using a Git command, but you cannot create and activate a new environment. You must create an environment using the `magento-cloud environment:branch <branch-name>` command for the environment to become _active_. Alternatively, you can use the Project Web Interface to create active environments. See [Cloud CLI reference](../dev-tools/cloud-cli-overview.md#git-commands).

**To clone a project `master` environment**:

1. Log in to your local workstation with a [file system owner](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) account.

1. Change to the web server or virtual host _docroot_ directory.

1. Log in using the `magento-cloud` CLI.

   ```bash
   magento-cloud login
   ```

1. List your projects.

   ```bash
   magento-cloud project:list
   ```

1. Clone a project.

   ```bash
   magento-cloud project:get <project-ID>
   ```

   When prompted provide a directory name.

1. Change to the `magento2` directory.

1. List available environments for the project.

   ```bash
   magento-cloud environment:list
   ```

   >[!IMPORTANT]
   >
   >The `magento-cloud environment:list` command displays environment hierarchies, whereas the `git branch` command does not.

1. Fetch the remote branches.

   ```bash
   git fetch origin
   ```

1. Pull updated code.

   ```bash
   git pull origin <environment-ID>
   ```

>[!TIP]
>
>See [Integrations](../integrations/overview.md) for information about using Git-based hosting services with Adobe Commerce on cloud infrastructure.



## Create a branch for development

After cloning your project and updating the Adobe Commerce administrator account configuration, you can branch for development. As stated earlier, you must create an environment using the `magento-cloud environment:branch <branch-name>` command or the Project Web Interface for the environment to become _active_.

-  For [Starter](../architecture/starter-develop-deploy-workflow.md#clone-and-branch), consider creating a branch for `staging`, then create a development branch based on the `staging` branch.
-  For [Pro](../architecture/pro-develop-deploy-workflow.md#development-workflow), create development branches based on the `Integration` branch.

**To create a development branch**:

1. On your local workstation, change to your project directory.

1. Create an environment based on the branch recommended for your project workflow.

   ```bash
   magento-cloud branch <new-environment-name> integration
   ```

1. Update dependencies.

   ```bash
   composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
   ```

1. [_optional_] Create a [snapshot](../storage/snapshots.md) of the environment.

### Merge a branch

After completing development, merge this branch to the parent:

1. Commit and push code changes:

   ```bash
   git add -A && git commit -m "Add message here"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Merge with the parent environment:

   ```bash
   magento-cloud environment:merge <environment-ID>
   ```

### Delete an environment

Only delete an environment if you are certain that you no longer need it. You cannot recover an environment after you delete it.

>[!WARNING]
>
>You cannot delete the `master` branch of any project.

You must be a project administrator, environment administrator, or Account Owner to perform this task. See [Manage user access to Cloud projects](../project/user-access.md).

When you delete an environment, the environment is set to _inactive_. The code is still available in the Git branch, but no longer contains the services or the database. To delete the environment completely, you must also delete the corresponding remote Git branch.

**To delete an environment**:

1. On your local workstation, change to your project directory.

1. Fetch updates from the remote server.

   ```bash
   git fetch
   ```

1. Delete the environment branch.

   ```bash
   magento-cloud environment:delete <environment-ID>
   ```

   Optionally, you can delete more than one environment at a time by adding multiple environment IDs to the delete command.

   ```bash
   magento-cloud environment:delete <environment-1-ID> <environment-2-ID>
   ```

1. Respond to the prompts to delete the local environment and the corresponding remote environment.

   ```terminal
   The environment <environment-ID> is currently active: deleting it will delete all associated data.
   Are you sure you want to delete the environment <environment-ID>? [Y/n]
   ```

   Deleting the environment places it in an _inactive_ state.

   ```terminal
   Delete the remote Git branch too? [Y/n]
   ```

   Deleting the remote Git branch removes the environment from the project.

1. Wait for the environment to delete.

   ```terminal
   Deleting environment <environment-ID>
   Waiting for the activity...
     Deleting environment <project-id>-<environment-ID>-xxxxxx

     [============================]  1 min (complete)
   Activity ID succeeded
   Deleted remote Git branch <environment-ID>
   Run git fetch --prune to remove deleted branches from your local cache.
   ```

>[!TIP]
>
>To activate an inactive environment, use the `magento-cloud environment:activate` command.

## Interact with remote environments

After you [set up SSH keys](../development/secure-connections.md), you can [connect from your local workspace to a remote environment](../development/secure-connections.md#connect-to-a-remote-environment) and interact with your project services and modify settings.
