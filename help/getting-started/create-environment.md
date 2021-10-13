---
title: Create an environment
description: Create a development environment and learn about images and environment types.
---

# Create an environment

An _environment_ is a single cluster of virtual machines that support services for customizing, testing, and deploying the Commerce application. Your program can have one production environment, one staging environment, and one or more development (non-production) environments.

As a part of the initial program setup, you must create a _development_ environment to deploy a pre-built Commerce image from the code repository.

**To create an environment**:

1. In the program UI, click **[!UICONTROL Add Environment]**.

1. Select **Development** from the _[!UICONTROL Environment type]_ list.

1. Add an environment _name_ and _description_, choose a _[!UICONTROL Cloud region]_, and click **[!UICONTROL Save]**.

1. The new environment is in the _[!UICONTROL Environments]_ list and displays the _Coming Up_ status.

## Details view

Your Cloud Manager Program Overview page and Environments page contain a list of environment names with their storefront URL, region, and status. Access the (...) shortcut menu to the right of any environment to choose **[!UICONTROL View Details]**, **[!UICONTROL Download Logs]**, or **[!UICONTROL Delete]**. You can view details about an environment using the Cloud Manager program UI or the CLI.

### View environment details in program

The environment detail page displays basic information about the environment, such as the Commerce application version, the region, and the storefront URL.

Each environment contains three segments:

- **Core Commerce**—contains the Commerce application and filesystem
- **Commerce services**—contains the services that support the application, such as Elasticsearch, RabbitMQ, and others
- **Database Services**—provides a persistent storage service

You have the option of applying one of your saved IP allowlists to the environment.

### View environment details at the command line

```bash
aio cloudmanager:program:list-environments
```

Example response:

```terminal
Environment Id Name         Type Description
123456         sample-dev   dev  Testing environment
```

>[!TIP]
>
> Learn how to change the default admin URL to reduce target attacks.
>
>**Next step**: [Access the storefront and change the admin URL](access-storefront.md)
