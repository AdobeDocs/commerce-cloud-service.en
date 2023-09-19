---
title: Cloud infrastructure project
description: Read an overview about the Adobe Commerce on cloud infrastructure Project Web Interface and learn how to access the account settings.
exl-id: ae862898-9b4d-45ed-b370-e82cc6f99017
---
# Cloud infrastructure project

The Adobe Commerce on cloud infrastructure project includes all code in Git branches, associated environments, and scripts to deploy the Commerce application. Environments contain services to support the Commerce application, including a database, web server, and caching server.

Adobe provides a Project Web Interface and developer tools to fully manage all aspects of your project. You, as the account owner, have full access to all environments.

## Project Web Interface

The Project WI provides a more modern, user-friendly experience and lays the foundation for future interface enhancements.

The Project Web Interface provides interactive methods to build, manage, and deploy Commerce code. [Log in to the Project Web Interface](https://console.magento.cloud) to view your project list. You can only see projects that you have permission to access as an admin or for specific environment types. If you are an Adobe Solutions Partner, you may see multiple projects for clients that you support.

>[!TIP]
>
>If you do not see any projects, you must contact the [Account Owner or Super User](../project/user-access.md) associated with the project and request access. For first-time users, see the [Onboarding topic](../../get-started/onboarding.md#project-web-interface) in the _Get started_ guide.

For **Starter** projects, there is a hierarchy of branches starting from `master` (Production). Any branch that you create display as children from the `master` branch. Adobe recommends creating a `staging` branch, then create an `integration` branch for development. See [Starter architecture](../architecture/starter-architecture.md).

For **Pro**, there is a hierarchy of branches starting from `production` to `staging` to `integration`. The ![Enterprise icon](../../assets/icon-deploy.png) icon indicates that the branch deploys to a dedicated server. Any branches that you create display as children of the `integration` branch. See [Pro architecture](../architecture/pro-architecture.md).

### Access storefront

Each active environment has a storefront. Select an environment from the top navigation and click the link in the environment Overview box. Also, there is a **[!UICONTROL URLs]** list on the right-had side above the Activity list.

The Web Access URL may include the following:

```terminal
https://<branch>-<unique-ID>-<project-ID>.<region>.magentosite.cloud/
```

- **Unique ID** = 7 random alpha-numeric characters
- **Project ID** = 13-character project ID
- **Region** = AWS or Azure region name, see [Regional IP addresses](regional-ip-addresses.md)

The Pro Production and Staging environments include three nodes that you can access using the following links:

-  Load balancer URLs:

    -  `http[s]://<your-domain>.c.<project-ID>.ent.magento.cloud`
    -  `http[s]://<your-staging-domain>.c.<project-ID>.ent.magento.cloud`

-  Direct access to one of the three redundant servers:

    -  `http[s]://<your-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`
    -  `http[s]://<your-staging-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`

   The production URL is used by the content delivery network (CDN).

## Settings

Open the _Settings_ panel by clicking on the configure icon.

![configure project icon](../../assets/icon-configure.png)

### Project settings

Click **[!UICONTROL Project Settings]** to manage users, deploy keys, and variables associated with the project. You can set the following configuration options for each project:

| Option       | Description                                                                                                                                        |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| General      | Manage the timezone for use with scheduling backups or maintenance.  |
| Access       | Manage user access to project and environment types. See [Manage user access](user-access.md).                                        |
| Certificates | View a list of the SSL certificates associated with the project.                                                                                   |
| Deploy Key   | Add and view the public key to the project code repository.                                                                                        |
| Domains      | Add a domain name to the project. See [Manage domains](../cdn/fastly-custom-cache-configuration.md#manage-domains).                                |
| Integrations | Add and manage [integrations](../integrations/overview.md), such as health notifications and webhooks. |
| Variables    | Add project-level variables that are available at build and runtime in all environments. See [Variable levels](../environment/variable-levels.md). |

{style="table-layout:auto"}

### Environment settings

Click **[!UICONTROL Environments]** and select a specific environment to view and manage variables, domains, and other settings. You can set the following configuration options for each environment:

| Option    | Description                                            |
| --------- | ------------------------------------------------------ |
| General   | Configure display name, environment type, and parent environment.<br>Toggle different environment settings:                 |
|           | **Enable outgoing emails**: Setting this option to `On` enables support for sending emails from the environment using the SMTP protocol. See [Outgoing emails](outgoing-emails.md). |
|           | **Hide from search engines**: Setting this option to `On` indicates do not index and ignore the site to search engine indexers. |
|           | **HTTP access control**: Setting this option to `On` enables you to configure security for the Project Web Interface using a login and IP address access control. |
|           | Status is `active` or `inactive`. Most of your work is in an active environment. You can deactivate or delete environment. |
| Variables | View, create, and manage environment variables available for the environment at runtime. See [Variable levels](../environment/variable-levels.md). |
| Domains   | View a list of configured routes. See [Configure routes](../routes/routes-yaml.md). |

{style="table-layout:auto"}

>[!WARNING]
>
>**DO NOT** use the HTTP access control method for securing Pro Staging and Production environments. This breaks Fastly caching. Instead, use the [Blocking](../cdn/fastly-vcl-blocking.md) feature available in the Fastly CDN for Adobe Commerce.

## Fastly and New Relic credentials

Your project includes [Fastly](../cdn/fastly.md) and [New Relic](../monitor/new-relic-service.md). The project details display information for your project plan and important licenses and tokens for these integrations. Only the License Owner has initial access to the credentials and services. Provide these credentials to technical and developer resources as needed.

-  [Fastly](https://www.fastly.com/) provides content delivery (CDN), image optimization, and security services (DDoS and WAF) for your Adobe Commerce on cloud infrastructure projects. See [Get Fastly credentials](../cdn/fastly-configuration.md#get-fastly-credentials).

-  [New Relic](../monitor/new-relic-service.md) provides application metrics and performance information for Staging and Production environments.

**To review your integration tokens, IDs, and more**:

1. Log in to [your account](https://console.magento.cloud)

1. In the upper right corner, click your name and **Account settings**.

   ![Go to account settings](../../assets/ui-account-settings.png)

1. On the _Projects_ tab, click **View Details** for your project to open general settings and plan details.

   ![View your project details](../../assets/ui-view-details.png)

1. On your project details page, scroll to and expand the **New Relic** and **Fastly** sections to review service credentials.

   ![Your New Relic credentials](../../assets/ui-service-details.png)
