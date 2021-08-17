---
title: Tour the Commerce Program
description: Quick tour of the Cloud Manager UI for Commerce.
---
# Tour the Commerce program

The Adobe Cloud Manager dashboard is a hub for your cloud-based programs and products. 
If you are a developer and you have an Adobe ID and belong to an organization, your System Administrator can then grant you access to the Cloud Manager product. 

Sign in to [Adobe Experience Cloud][cm-dash] for your organization and select **[!UICONTROL Programs & Products]**.

A Commerce _program_ contains a code repository, the latest Commerce images, and Cloud-native technologies to help you create custom environments and pipelines.

**To add a Commerce program:**

1. From the Cloud Manager **Programs & Products** card view, click **[!UICONTROL Add program]** to create a Commerce program.

1. Choose **[!UICONTROL Adobe Commerce]** for your new program and continue through the steps.

1. Provide a **[!UICONTROL Program name]** and select the **[!UICONTROL Set up for production]** objective. Optionally, you can upload an image for easy program identification.

    >[!IMPORTANT]
    >
    >   Will there be multiple objectives to choose from?


1. Click **[!UICONTROL Continue]**. The new Program card shows a "Setting up program" status.

## Program overview

Your new program opens with the _[!UICONTROL Program overview]_ page, which is a summary board that displays the status of your resources and provides opportunities to learn and do more. Program provisioning takes time; after the setup is complete, you should see a What-is-next activity and three main sections: **[!UICONTROL Environments]**, **[!UICONTROL Pipelines]**, and **[!UICONTROL Useful Resources]**.

![Commerce overview](../assets/program-newdashboard.png)

The What-is-next activity guides you through the next steps. The steps that follow may be based on the objective chosen when creating your Commerce program in Cloud Manager.

- For a new Commerce program, you must create a branch and a project. Click **[!UICONTROL Create]** and follow the steps.
- For a development sandbox, the Program setup script automatically builds a new Project, environment, and non-production pipeline ready for you to use.

Next step: [Access and Clone the Git repository](clone-git-repo.md)

<!-- link definitions -->
[cm-dash]: https://my.cloudmanager.adobe.com
