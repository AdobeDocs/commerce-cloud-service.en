---
title: Manage Pipelines
description: An introduction to pipeline management with Cloud Manager UI for Commerce.
---
# Manage pipelines

A pipeline automates the build and deploy process. The pipeline performs actions using a Git branch, so it cannot be set up until the code repository has at least one branch and the Program Setup is complete.

There are three types of pipelines:

-  **Build-only**—Build the target Git branch and create a _build artifact_ with a unique ID.

-  **Deploy-only**—Deploy a build artifact in the target environment.

-  **Build and deploy**—Build and deploy code from an existing environment.

When you create a pipeline, you must specify a name, a Git branch, and the action, or trigger type, that begins executing the pipeline. You can activate a pipeline **manually** when you need it, or when a particular **Git change** occurs, or based on a preset **schedule**.

List current or historical pipeline executions.

```bash
aio cloudmanager:execution:get-step-details ID ID
```
