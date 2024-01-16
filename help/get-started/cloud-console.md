---
title: Cloud Console
description: Learn about the Cloud Console for Adobe Commerce on Cloud infrastructure.
recommendations: noDisplay, catalog
exl-id: c19a36b6-e5e8-461c-a82c-68b7bf121999
---

# Cloud Console

The Cloud Console provides interactive methods to build, manage, and deploy Commerce code. The Cloud Console is a more modern, user-friendly experience and lays the foundation for future interface enhancements.

[Log in to the Cloud Console](https://console.adobecommerce.com) to view your project list.

## New features

The new or improved features include:

- Clear overview of project and environment characteristics
- Activity stream with sortable history
- Manual backup management and history for Starter projects
- Enhanced log views
- Sortable lists
- Simple forms and guidance to add integrations
- Web Content Accessibility Guidelines (WCAG) compliance

![Cloud Console](../assets/CloudConsole.svg)

The new or improved features are as follows:

| Feature        | Improvements                        |
| -------------- | ----------------------------------- |
| [Activity stream](../cloud-guide/project/activity-stream.md) | Interact with a sortable list of running, pending, or historical actions. Select an activity and view logs or cancel a running build. |
| [Project and Environment overviews](../cloud-guide/project/overview.md#project-overview) | Open your project to find a new overview of project details and environment list. The environment overview provides more details about the environment status. application access, and recent activities. |
| [Integration forms](../cloud-guide/integrations/overview.md) | Use simple forms and guidance to add integrations, such as Bitbucket or Slack notifications. |
| [Project list](../cloud-guide/project/overview.md#cloud-console) | The _All projects_ view lists all projects that you have permission to access. You can click **[!UICONTROL Show filters]** and filter your project list by type, region, or plan. |
| [Variable visibility options](../cloud-guide/environment/variable-levels.md) | Limit the visibility of a project-level or environment-level variable during build or runtime. |

<!-- The following are features yet to be activated:
| **Apps and services topology** | The Apps & Services topology is visible on Project and Environment views. This interactive diagram allows you to select a service and view the relationship details, such as name, type, version, port, and more. Click **[!UICONTROL View details]** to access the overview and configuration panel for each service. | -->

## Console questions

**_Where can I find the Snapshots feature_**?

For Starter projects, the Snapshots feature is now called _Backups_. You can create a manual backup of your Starter environment from the Cloud Console or create a snapshot from the Cloud CLI. You must have an Admin role for the environment.

Select an environment from the project navigation bar. The environment must be active. Select the **[!UICONTROL Backups]** tab. Currently, this option is not available for Pro environments.

**_Where is the list of configured routes for the environment_**?

You can find the list of configured routes on the _Services_ tab for an environment.

Select an environment from the project navigation bar. Select the **[!UICONTROL Services]** tab. The **Router** overview displays the configured routes. Currently, you cannot add a route from the new Cloud Console.

## Account menu

In the top right-hand corner is your account menu. Click the down arrow to access the menu and select **[!UICONTROL My Profile]**. In the _My Profile_ view, you can control your user details and display settings, manage [security authentication](../cloud-guide/project/user-access.md#user-authentication-requirements), [API tokens](../cloud-guide/project/user-access.md#create-an-api-token), and [SSH keys](../cloud-guide/development/secure-connections.md).
