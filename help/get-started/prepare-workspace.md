---
title: Prepare your workspace
description: Learn how to gather credentials and set up a local workspace.
recommendations: noDisplay, catalog
---

# Prepare your workspace

This section walks through the steps for first-time merchants with Adobe Commerce, SIs, and existing merchants moving to the cloud. If you already completed some of these steps or have an existing Adobe Commerce developer environment, review the following for expected results and continue to the next step. Some configurations and workflows differ from the typical on-premises installation.

## Gather credentials

Before setting up a workspace, gather the following credentials and accounts:

- **Authentication keys (Composer keys)**

  Authentication keys are 32-character authentication tokens that provide secure access to the Adobe Commerce Composer repository (repo.magento.com), and any other Git services required for application development such as GitHub. Your account can have multiple authentication keys. For the workspace setup, start with one specific key for your code repository. If you do not have any keys, contact the Account Owner to create them, or create the [authentication keys](authentication-keys.md) yourself.

- **Cloud Project account**

  The Account Owner or Technical Admin (Super User) should invite you to the Adobe Commerce on cloud infrastructure project. When you receive the e-mail invitation, click the link and follow the prompts to create your account.

- **Adobe Commerce Encryption Key**

  When importing an existing system only, capture the encryption key used to protect your access and data for the database. For details on this key, see [Resolve issues with encryption key](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolve-issues-with-encryption-key.html)

## Launch a Docker environment

You can use the Docker environment to emulate the Adobe Commerce on cloud infrastructure Integration environment for local development. You need three essential components: an Adobe Commerce v2 template, Docker Compose, and Adobe Commerce on cloud infrastructure `ece-tools` package.

- [Docker architecture and common commands](../dev-tools/cloud-docker.md)
- [Launch Docker development environment](https://developer.adobe.com/commerce/cloud-tools/docker/setup/)

>[!TIP]
>
>For information about using Git-based hosting services with Adobe Commerce on cloud infrastructure, see [Integrations](../integrations/overview.md).

>[!TIP]
>
>For existing Commerce owners migrating to the Cloud infrastructure, learn how to import existing code to the cloud environment.
>
>**Next step**: [Import existing code](import-existing-code.md)
