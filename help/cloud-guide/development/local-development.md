---
title: Local development
description: Prepare for local development with an Adobe Commerce on cloud infrastructure project.
---

# Local development

Adobe Commerce on cloud infrastructure environments are **Read Only**, including all Starter environments and all Pro Integration, Staging, and Production environments. In a local development environment, you can write and test code prior to pushing it to an Integration environment for further testing and deployment to Staging and Production. You must develop in a local workstation using a cloned Integration environment and push changes to the remote, read-only Adobe Commerce on cloud infrastructure Git repository. You can choose one of two methods:

## Gather credentials

Prior to setting up a workspace, gather the following credentials and accounts:

-  **Authentication keys (Composer keys)**

    Authentication keys are 32-character authentication tokens that provide secure access to the Adobe Commerce Composer repository (repo.magento.com), and any other Git services required for application development such as GitHub. Your account can have multiple authentication keys. For the workspace setup, start with one specific key for your code repository. If you do not have any keys, contact the Account Owner to create them, or create the [authentication keys](authentication-keys.md) yourself.

-  **Cloud Project account**

    The Account Owner or Technical Admin (Super User) should invite you to the Adobe Commerce on cloud infrastructure project. When you receive the e-mail invitation, click the link and follow the prompts to create your account. See [Onboarding](../../get-started/onboarding.md) or [Access the Project Web Interface](../project/overview.md) for details.

-  **Adobe Commerce Encryption Key**

    When importing an existing system only, capture the encryption key used to protect your access and data for the database. For details on this key, see [Resolve issues with encryption key](https://support.magento.com/hc/en-us/articles/360033978652)

## Launch a Docker environment

You can use the Docker environment to emulate the Adobe Commerce on cloud infrastructure Integration environment for local development. You need three, essential components: a Adobe Commerce v2 template, Docker Compose, and Adobe Commerce on cloud infrastructure `ece-tools` package.

-  [Docker architecture and common commands](https://devdocs.magento.com/cloud/docker/docker-development.html)
-  [Launch Docker development environment](https://devdocs.magento.com/cloud/docker/docker-config.html)
