---
title: Tour the Commerce program
description: Quick tour of the Cloud Manager UI for Commerce.
---
# Tour the Commerce program

The Adobe Cloud Manager dashboard is a hub for your cloud-based programs and products. If you are a developer with an Adobe ID and belong to an organization, your System Administrator can grant you access to the Cloud Manager product.

Sign in to [Adobe Experience Cloud][cm-dash] for your organization and select **[!UICONTROL Programs & Products]**.

A Commerce _program_ contains a code repository, the latest Commerce images, and Cloud-native technologies to help you create custom environments and pipelines.

**To add a Commerce program:**

1. From the Cloud Manager **Programs & Products** card view, click **[!UICONTROL Add program]** to create a Commerce program.

1. Choose **[!UICONTROL Adobe Commerce]** for your new program and continue through the steps.

1. Provide a **[!UICONTROL Program name]** and select the **[!UICONTROL Set up for production]** objective. Optionally, you can upload an image for easy program identification.

1. Click **[!UICONTROL Continue]**. The new Program card shows a "Setting up program" status.

## Program overview

Your new program opens with the _[!UICONTROL Program Overview]_ page, which is a summary board that displays the status of your resources and provides opportunities to learn and do more. Program provisioning takes time; after the setup is complete, you should see a suggested activity space and three main tiles: **[!UICONTROL Environments]**, **[!UICONTROL Pipelines]**, and **[!UICONTROL Useful Resources]**.

![Commerce overview](../assets/program-newdashboard.png)

### Suggested action

The suggested action space guides you through the next steps. The steps that follow may be based on the objective chosen when creating your Commerce program in Cloud Manager. For Getting started, you essentially have a development sandbox; the Program setup script automatically builds a new Project, environment, and non-production pipeline ready for you to use.

### Program tabs

There are three additional tabs or views for your program:

The _Environments_ tab provides a list of all environments for your program. Here you can add an environment, manage SSL certificates, and IP allowlists, and you can add a domain name for a specific environment. Choosing a specific environment opens a details page where you can apply IP allowlists and see the status of specific segments, such as database services.

The _Activity_ tab is a log of events with status, duration, and actions you may be able to take.

The _Learn_ tab shows you relevant tiles that lead you to learning content, such as Commerce or Cloud Manager documentation and tutorials.

The _Pipelines_ tab is available after you create a pipeline.

>[!TIP]
>
>It's time to see some Commerce code.
>
>**Next step**: [Access and Clone the Git repository](clone-git-repo.md)

<!-- link definitions -->
[cm-dash]: https://my.cloudmanager.adobe.com
