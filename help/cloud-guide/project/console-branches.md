---
title: Manage branches with the Project Web Interface
description: Learn how to manage the environment branches for Adobe Commerce on cloud infrastructure using the Project Web Interface.
role: Developer
feature: Cloud, Install
exl-id: 2c4ef149-fdb9-473f-91fd-5e6421ac5a43
---
# Manage branches with the Project Web Interface

You can manage your environments using either the Project Web Interface or the `magento-cloud` CLI. Your project files are stored in a Git repository. You can use Git commands to manage your code, but the `magento-cloud` CLI is designed to interact with platform features whereas the Git commands do not. See [Git commands](../dev-tools/cloud-cli-overview.md#git-commands) in the cloud CLI topic.

This topic discusses how to use the Project Web Interface to:

- Add or delete an environment
- Sync (`git pull`) from the parent environment
- Merge (`git push`) to the parent environment

>[!TIP]
>
>You cannot create branches from Pro Staging and Production environments. You can branch from the `master` branch.

## Create an environment

The branching strategy uses a common Git workflow where you develop code and add extensions in a development branch. See [Starter](../architecture/starter-architecture.md) and [Pro](../architecture/starter-develop-deploy-workflow.md) architecture overviews.

- For Starter, create a `staging` branch from the `master` branch, then branch from `staging` for development.
- For Pro, create a development branch from the `Integration` environment.

Your account supports a limited number of active Git branches and an unlimited number of inactive development branches. Manage active and inactive branches by adding or deleting a branch. When deleted, a branch is deactivated and remains listed in the project branches list as _inactive_. You can activate the inactive branch later or you can [delete the branch](../dev-tools/cloud-cli-overview.md#) using the CLI.

If you need additional environments for development, enter a [Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

**To add a branch**:

1. Log in to [the Project Web Interface](https://console.magento.cloud).

1. Select a project from the _All projects_ list.

1. Select an environment.

   >[!TIP]
   >
   >Your new branch is cloned from this environment. Choose a parent environment that is similar to the environment that you are about to create.

1. Click **[!UICONTROL Branch]**.

   ![Create a branch](../../assets/icon-branch.png){width="150"}

1. In the _Branching from ..._ form, enter a branch name.

   The environment _name_ is different from the environment _ID_ only if you use spaces or capital letters in the environment name. An environment ID consists of all lowercase letters, numbers, and allowed symbols. Capital letters in an environment name are converted to lowercase in the ID; spaces in an environment name are converted to dashes.

   An environment name **cannot** include characters reserved for your Linux shell or for regular expressions. Forbidden characters include curly braces (`{ }`), parentheses, asterisk (`*`), angle brackets (`>`), ampersand (`&`), percent (<code>%</code>), and other characters.

1. Select an **[!UICONTROL Environment type]**.

1. Click **[!UICONTROL Create Branch]**.

1. Wait while the environment deploys.

   During deployment, the environment status is  **In process**. After a successful deployment, the status changes to a green check mark for **success**.

## Delete an environment

Before you can delete an environment, you must deactivate it. Once an environment is inactive, you can delete it.

**To deactivate an environment**:

1. Log in to [the Project Web Interface](https://console.magento.cloud).

1. Select a project from the _All projects_ list.

1. Select the environment from the navigation bar _Environment_ list.

1. Click the configure icon on the right side of the navigation bar, which opens the environment settings.

1. On the _[!UICONTROL General]_ tab, scroll down to the _[!UICONTROL Deactivate environment]_ section and click **[!UICONTROL Deactivate environment and delete data]** and follow the instructions.

## Sync an environment

Syncing an environment (or branch) is the same as `git pull origin <parent>`. You can sync to get updated code from a parent environment. You can use this feature through the interface for all Starter and Pro environments.

For Pro plan, you can sync from Staging and Production to your `master` branch. This sync only pulls and pushes code, not data. To sync data, dump the database data and push it to another environment's database. See [Migrate and deploy static files and data](/help/cloud-guide/deploy/staging-production.md#migrate-static-files).

**To sync an environment**:

1. Log in to [the Project Web Interface](https://console.magento.cloud).

1. Select a project from the _All projects_ list.

1. In the environment list, click the name of the branch to sync.

1. Click (sync).

    ![Sync an environment](../../assets/icon-sync.png){width="150"}

1. Select the items to sync.

   - Replace the data—(data and files) syncs changes in the database and content files from the parent branch.
   - Merge—(code) syncs updated code from the parent branch.

   This also builds a CLI command for you to copy and use.

1. Click **Sync**.

## Merge with parent environment

Merging an environment (or branch) is the same as `git push origin`. You merge to push updated code from an environment to its parent environment. You can merge this code to `master`. You can deploy to Staging and Production using the `merge` command.

**To merge with the parent environment**:

1. Log in to [the Project Web Interface](https://console.magento.cloud).

1. Select a project from the _All projects_ list.

1. In the environment list, click the name of the branch to merge.

1. Click (merge).

   ![Merge an environment](../../assets/icon-merge.png){width="150"}

1. Click **Merge** and confirm the action.

## View logs

Through the Project Web Interface, you can review various logs for environments including build, deploy, and deployment history.

For **Starter**, you can review build and deploy logs and the deployment history. These environments include the `master` (Production) branch and all branches created from it.

For **Pro**, you can review the following logs in each environment:

- Integration—Build and deploy and deployment history
- Staging—Build logs and deployment history. Use SSH to log into the server to view deploy logs.
- Production—Build logs and deployment history. Use SSH to log into the server to view deploy logs.

**To view logs in the Project Web Interface**:

1. Log in to [the Project Web Interface](https://console.magento.cloud).

1. Select a project from the _All projects_ list.

1. Select an environment.

   The environment view provides an [Activity list](activity-stream.md) that shows _recent_ events, one entry per action attempted including syncs, merges, branches, snapshots, and more. Click **All** for the full deployment history.

1. To view the build log, select the Success or Failure link per deployment record on the account.

>[!TIP]
>
>Click the **Filter by** icon for a drop-down list and select the type of messages to view.

## Pull code from a private Git repository

Your Adobe Commerce on cloud infrastructure project can include code from a private Git repository. For example, you may have code for a custom module or theme in a private repo. To do so, you must add your project's public SSH key to your private Git repository and update your project `composer.json` file.

To add a deployment key to your private GitHub repository, you must be the administrator of that repository. GitHub allows you to use a deploy key for one repository only.

If you prefer that your project accesses multiple repositories, you can attach an SSH key to an automated user account. Because this account is not used by a human, it is referred to as a [machine user](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys). Add the machine account as a collaborator or add the machine user to a team with access to the repositories.

>[!INFO]
>
>Adobe recommends adding and merging this code to your project Git repositories. If you do not configure the connection, you may experience build issues.

**To find your SSH public key**:

1. Log in to [the Project Web Interface](https://console.magento.cloud).

1. Select a project from the _All projects_ list.

1. Click the configuration icon on the right side of the navigation bar.

1. In _Project Settings_, click **[!UICONTROL Deploy Key]**.

1. Copy the deploy key to the clipboard.

Use your deploy key in one of the following Git-based methods:

>[!BEGINTABS]

>[!TAB GitHub]

### Enter your GitHub deploy key

On GitHub, deploy keys are read-only by default.

**To enter your project public key as a GitHub deploy key**:

1. Log in to your GitHub repository as the administrator.
1. Click the repository **[!UICONTROL Settings]** tab.

   >[!NOTE]
   >
   >If you do not see this option, you are not logged in as a repository administrator, and you cannot complete this task. Ask your GitHub repository administrator to do this.

1. On the _Settings_ tab in the left navigation bar, click **[!UICONTROL Deploy Keys]**.
1. Click **[!UICONTROL Add deploy key]**.
1. Follow the prompts.

In `composer.json`, use the `<user>@<host>:<.git</code>` format, or `ssh://<user>@<host>:<port>/<path>.git` if using a non-standard port.

>[!TAB Bitbucket]

### Enter your Bitbucket deploy key

**To enter your project public key as a Bitbucket deploy key**:

1. Log in to your Bitbucket repository as the administrator.
1. In the left navigation bar, click **[!UICONTROL Settings]**.
1. Click General > **[!UICONTROL Deployment Keys]**.
1. Click **[!UICONTROL Add Key]**.
1. Follow the prompts.

>[!TAB GitLab]

### Enter your GitLab deploy key

**To add the public SSH key for your project as a GitLab deploy key**:

1. Log in to your GitLab repository as the owner.
1. Verify that the _Pipelines_ option is enabled for your project:

   1. In the project settings, expand the **[!UICONTROL Visibility, project, features, permissions]** section.
   1. If necessary, click **[!UICONTROL Pipelines]** to enable the option.

1. Add your public SSH key to the CI/CD settings.

   1. In the left navigation, click Settings > **[!UICONTROL CI / CD]**.
   1. Click Deploy Keys **Expand** to configure the key.
   1. In the _Deploy Key_ form, add a deploy key name to the **[!UICONTROL Title]** field and paste your public SSH key in the **[!UICONTROL Key]** field.
   1. Click **[!UICONTROL Add Key]** to save the configuration.

>[!ENDTABS]

## Secure environments and branches

You can access your project and environments from any location through a web browser using the Project Web Interface. You may have security set for your Production environment, stores, and sites. This section helps you secure your Integration and Staging environments for strictly your developers, DBAs, and more.

>[!WARNING]
>
>**DO NOT** use the following methods for securing Pro Staging and Production environments. This breaks Fastly caching. Use the [Blocking](../cdn/fastly-vcl-blocking.md) feature available in the Fastly CDN for Adobe Commerce.

**To secure environments**:

1. Log in to your [Project Web Interface](https://console.magento.cloud).

1. Select a project from the _All projects_ list.

1. Select an environment and click the configuration icon on the navigation bar.

1. On the environment settings _General_ tab, click **ON** for **[!UICONTROL HTTP access control enabled]** to enable secure access. You can choose between credentials or IP addresses to filter for access.

1. To filter by credentials, click **[!UICONTROL Add Login]**, enter a username and password, and click **[!UICONTROL Add Login]** to add.

1. To filter by IP address, enter the IP addresses in a list with `deny` or `allow`. For example:

   ```text
   123.456.789.111/29 allow
   123.456.789.112/29 allow
   234.123.567.111/29 allow
   0.0.0.0/0 deny
   ```

1. Click **[!UICONTROL Save]**. This redeploys the environment to update security and settings. Adobe recommends testing the environment after completing security settings.
