---
title: Create a pipeline
description: Set up a build-and-deploy pipeline and learn about the CI/CD process.
---

# Create a pipeline

A _pipeline_ executes a set of instructions for building and deploying the Commerce application. Git branches and environments play an important role in the CICD process. The pipeline performs actions using a Git branch, so the pipeline cannot be set up until the code repository has at least one branch and the Program Setup is complete.

There are three types of pipelines:

- **Build + Deployment**—Select an environment and build and deploy the existing code.

- **Build only**—Select a Git branch and create a _build artifact_ with a unique ID.

- **Deployment only**—Select a target environment to deploy a build artifact.

When you create a pipeline, you must specify the pipeline type, a name, and a build trigger to activate the pipeline. Build triggers include "Manual" for activating on demand, or "On Git change" for activating when a particular Git change occurs.

**To create a Build + Deployment pipeline**:

1. In the Program Overview _Pipelines_ section, click **[!UICONTROL Add]**.

1. Select the **[!UICONTROL Build + Deployment]** pipeline type.

1. Type in a [!UICONTROL Pipeline Name].

1. Select the **[!UICONTROL Manual]** build trigger.

1. In the _Git Branch_ list, select a branch of code to build and deploy.

1. In the _Deployment Configuration_, select a target **[!UICONTROL Deployment Environment]**, such as a staging environment for testing the code with specific availability of services.

## Do something else

>[!TIP]
>
>**Next step**: [Build and deploy your store](build-and-deploy-store.md)
