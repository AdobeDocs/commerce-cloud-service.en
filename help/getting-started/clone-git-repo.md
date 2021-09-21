---
title:  Git repository
description: Clone the git code repository and apply credentials.
---
# Access and Clone the Git Repository

The _Git repository_ contains the source files to build and customize your Commerce application. Before you can clone the repository, you must install a [Git client][git]. A username, password generator, and repository URL are provided in your Cloud Manager program UI.

**To clone the Git repository**:

1. In the program UI, click **[!UICONTROL {} Access Repo Info]** in the _Access Git & Pull Code_ suggested action space, or in the _Pipelines_ tile.

1. Click **[!UICONTROL Generate password]**, which generates a personal access token (PAT) and is required to access the repository from the command line.
1. Make note of the Username, Password, and URL.
1. Copy the Git command line.
1. Open a terminal and paste the Git command line. You can append a new directory name for your program.

   ```bash
   $ git clone https://git.cloudmanager.adobe.com/tenant/programName-programID-uk30899/ MyProgram
   ```

1. When prompted, enter your Username and Password.

   ```terminal
   Cloning into 'DocsAug20'...
   Username for 'https://git.cloudmanager.adobe.com': <user-org-com>
   Password for 'https://user-org-com@git.cloudmanager.adobe.com': <password>
   ...
   ```

1. Change to the cloned repository directory.

## Initial file structure

All Commerce repositories include essential files for application configuration:

| File                      | Description |
| ------------------------- | ----------- |
| `/.magento/routes.yaml`   | Configuration file that determines how the application processes incoming HTTP and HTTPS requests, configure caching, redirects, and server-side includes. |
| `/.magento/services.yaml` | Configuration file that defines services, such as MySQL, Redis, and ElasticSearch. |
| `/app`                    | The `code` folder is used for custom modules. The `design` folder is used for custom themes. The `etc` folder contains configuration files for the application. |
| `/m2-hotfixes`            | Used for custom patches. |
| `/update`                 | A service folder used by the support module. |
| `.gitignore`              | Specify which files and directories to ignore. |
| `.magento.app.yaml`       | Configuration file that defines how to build and deploy the application, including services, hooks, and cron jobs. |
| `composer.json`           | Fetches the Commerce code and the necessary configuration scripts to build and deploy the application. |
| `composer.lock`           | Stores version dependencies for every package. |
| `magento-vars.php`        | A file used to define multiple stores and sites using variables. |

## Managing Git

There are no AIO CLI commands for managing your Git code repository. You can use standard Git commands for maintaining your cloned instance. Use the following command to verify your local and remote configuration:

```bash
git remote show origin
```

>[!TIP]
>
>At this point, you have cloned your new repository and downloaded the Commerce code. You are not connected to an environment. The next step helps you through setting up your CLI tools and connecting to the Cloud Manager program.
>
>**Next step**: [Set up and connect the CLI tools](connect-cli.md)

<!-- link definition -->
[git]: https://git-scm.com/downloads

