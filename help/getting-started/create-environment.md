---
title: Create an environment
description: Create a development environment and learn about images and environment types.
---

# Create a default environment

An _environment_ is a single cluster of virtual machines that support services for customizing, testing, and deploying the Commerce application. Your program can have one production environment, one staging environment, and one or more development (non-production) environments. As a part of the initial program setup, Cloud Manager creates a _development_ environment to deploy a pre-built Commerce image from the code repository.

Your Cloud Manager Program Overview page and Environments page contain a list of environment names with their storefront URL, region, and status. Access the (...) shortcut menu to the right of any environment to choose **[!UICONTROL View Details]**, **[!UICONTROL Download Logs]**, or **[!UICONTROL Delete]** .

## View environment details

The environment detail page displays basic information about the environment, such as the Commerce application version, the region, and the storefront URL.

Each environment contains three segments:

- **Core Commerce**—contains the Commerce application and filesystem
- **Commerce services**—contains the services that support the application, such as Elasticsearch, RabbitMQ, and others
- **Database Services**—provides a persistent storage service

You have the option of applying one of your saved IP allowlists to the environment.

## Customize the environment

>[!IMPORTANT]
>
>Discuss the environment variables?
>
>Perhaps this can be a separate topic...next task to customize environment?

### Troubleshooting

If an environment enters a failure state after applying a custom variable, remove the variable that was added and test if the environment remains in error.

>[!TIP]
>
>**Next step**: [Set up a non-production pipeline](create-pipeline.md)
