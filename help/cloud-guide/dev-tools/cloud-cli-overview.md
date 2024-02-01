---
title: Cloud CLI
description: Learn about the magento-cloud CLI and how it helps you to manage local development environments for your Adobe Commerce on cloud infrastructure project.
exl-id: 70dddd62-0269-4af4-bd2a-1a4fbf11a131
---

# Cloud CLI

The `magento-cloud` CLI tool enables developers and system administrators the ability to manage Cloud projects and environments, perform routines and run automation tasks. The `magento-cloud` CLI extends the features and functionality of the [Cloud Console](../../get-started/cloud-console.md). After you install the `magento-cloud` CLI on your local workstation, you can use it to manage your Adobe Commerce on cloud infrastructure Starter and Pro integration environments.

**To install the `magento-cloud` CLI**:

1. On your local workstation, change to the directory where you intend to clone the Cloud project and where the [file system owner](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) has _write_ access.

1. Install the `magento-cloud` CLI.

   ```bash
   curl -sS https://accounts.magento.cloud/cli/installer | php
   ```

1. Add `magento-cloud` CLI to the bash profile.

   ```bash
   export PATH=$PATH:$HOME/.magento-cloud/bin
   ```

1. Reload the updated bash profile.

   ```bash
   . ~/.bash_profile
   ```

1. To initiate the CLI, call `magento-cloud` and enter your Cloud account credentials when prompted.

   ```bash
   magento-cloud
   ```

   ```terminal
   Welcome to Magento Cloud!
   Please log in using your Magento Cloud account.
   Your email address or username:
   ```

1. Verify the `magento-cloud` command is in your path. The following example lists the available commands.

   ```bash
   magento-cloud list
   ```

## Common commands

Adobe designed these commands to manage Cloud integration environments and recommends that you run the `magento-cloud` CLI from a project directory, so that you can omit the `-p <project-ID>` parameter.

The following list of commonly used `magento-cloud` CLI commands includes required options only. You can use the `--help` option with any command to see more information.

| Command                              | Description                                        |
| ------------------------------------ | -------------------------------------------------- |
| `magento-cloud login`                | Log in to the project.                             |
| `magento-cloud list`                 | List the available commands for CLI tool.          |
| `magento-cloud environment:list`     | List the environments in the current project.      |
| `magento-cloud environment:checkout` | Check out an existing environment.                 |
| `magento-cloud environment:merge -e` | Merge changes in this environment with its parent. |
| `magento-cloud variables`            | List variables in this environment.                |
| `magento-cloud ssh`                  | Use SSH to connect to the remote environment.      |
| `magento-cloud url`                  | Open the Adobe Commerce storefront in a browser.   |
| `magento-cloud web`                  | Open the [!DNL Cloud Console].                    |

## Environment commands

The environment _name_ is different from the environment _ID_ only if you use spaces or capital letters in the environment name. An environment ID consists of all lowercase letters, numbers, and allowed symbols. Capital letters in an environment name are converted to lowercase in the ID; spaces in an environment name are converted to dashes.

An environment name _cannot_ include characters reserved for your Linux shell or for regular expressions. Forbidden characters include curly braces (`{ }`), parentheses, asterisk (`*`), angle brackets (`< >`), ampersand (`&`), percent (`%`), and other characters.

The `magento-cloud environment:list` command displays environment hierarchies, whereas `git branch` does not. If you have any nested environments, use the following:

```bash
magento-cloud environment:list
```

### Redeploy the environment

Trigger a redeployment without using a push. Verify and confirm the environment to redeploy. Do not use redeploy if there is a build in a pending state.

```bash
magento-cloud environment:redeploy
```

Sample response:

```terminal
Are you sure you want to redeploy the environment <environment-name>? [Y/n]
```

{{redeploy-warning}}

## Git commands

You may notice that some of these commands are similar to Git commands. The `magento-cloud` commands directly connect to the Git-based Cloud project with additional features. If you create a branch without using the `magento-cloud` CLI, it is not "activated" and does not automatically build when you push changes to the remote environment. The `magento-cloud` CLI command includes activation.

To create a branch, use the `magento-cloud` command so the branch is activated.

```bash
magento-cloud environment:branch <new-name> <parent-branch>
```

For branch status:

-  Use the `magento-cloud env` command to view a list of the environment branches and their status: active or inactive.
-  Use the `magento-cloud environment:activate` command to activate an environment branch.

Push an empty Git commit to trigger a deployment. For example:

```bash
git commit --allow-empty -m "redeploy" && git push <branch-name>
```

Some actions, such as adding a user, do not result in deployment.

### Create an environment branch

The following steps demonstrate using the CLI and Git commands interchangeably to manage your local environment:

1. On your local workstation, change to your project directory.

1. Switch to the [file system owner](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html).

1. Log in to your project.

   ```bash
   magento-cloud login
   ```

1. List your projects.

   ```bash
   magento-cloud project:list
   ```

1. List environments in the project. Every environment includes an active Git branch that contains your code, database, environment variables, configurations, and services.

   ```bash
   magento-cloud environment:list
   ```

   >[!NOTE]
   >
   >It is important to use the `magento-cloud environment:list` command because it displays environment hierarchies, whereas the `git branch` command does not.

1. Fetch origin branches to get the latest code.

   ```bash
   git fetch origin
   ```

1. Checkout, or switch to, a specific branch and environment.

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

   Git commands only checkout the Git branch. The `magento-cloud checkout` command checks out the branch and switches to the active environment.

   >[!TIP]
   >
   >You can create an environment branch using the `magento-cloud environment:branch <environment-name> <parent-environment-ID>` command syntax. It may take some additional time to create and activate an environment branch.

1. Use the environment ID to pull any updated code to your local. This is not necessary if the environment branch is new.

   ```bash
   git pull origin <environment-ID>
   ```

1. (_Optional_) Create a [snapshot](../storage/snapshots.md) of the environment as a backup.

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

## Update the CLI

The `magento-cloud` CLI checks for available updates when you log in, but you can check for updates using the `self:update` command. If there is an update available, follow the instructions to update the CLI.

If your `magento-cloud` CLI is up to date, you see the following response:

```bash
magento-cloud update
```

```terminal
Checking for Magento Cloud CLI updates (current version: X.XX.X)
No updates found
```
