---
title: Prepare your workspace
description: Learn how to gather credentials for your Commerce cloud project and set up a development workspace.
recommendations: noDisplay, catalog
---

# Prepare your workspace

Whether you are a first-time merchant or an existing Adobe Commerce merchant moving to the cloud infrastructure, begin to prepare your workspace with these steps. If you already completed some of these steps or have an existing Adobe Commerce developer environment, review the following for expected results and continue to the next step. Some configurations and workflows differ from the typical on-premises installation.

## Gather credentials

Before setting up a workspace, gather the following credentials and accounts:

- **Authentication keys (Composer keys)**

  Authentication keys are 32-character authentication tokens that provide secure access to the Adobe Commerce Composer repository (repo.magento.com), and any other Git services required for application development such as GitHub. Your account can have multiple authentication keys. For the workspace setup, start with one specific key for your code repository. If you do not have any keys, contact the project owner, or create the [authentication keys](../cloud-guide/development/authentication-keys.md) yourself.

- **Cloud Project account**

  The Project Owner should invite you to the Adobe Commerce on cloud infrastructure project. When you receive the e-mail invitation, click the link and follow the prompts to create your account.

- **Adobe Commerce Encryption Key**

  When importing an existing system only, capture the encryption key used to protect your access and data for the database. For details on this key, see [Resolve issues with encryption key](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolve-issues-with-encryption-key.html)

## Developer tools

Install the `magento-cloud` CLI so that you can manage Cloud environments and run automation tasks.

### Launch a Docker environment

You can use the Docker environment to emulate the Commerce on cloud infrastructure `integration` environment for local development. You need three essential components: an Adobe Commerce v2 template, Docker Compose, and `ece-tools` package.

- [Docker architecture and common commands](../cloud-guide/dev-tools/cloud-docker.md)
- [Launch Docker development environment](https://developer.adobe.com/commerce/cloud-tools/docker/setup/)
- [ECE-Tools package](../cloud-guide/dev-tools/package-overview.md)

### Git-based services

For information about using Git-based hosting services with Adobe Commerce on cloud infrastructure, see [Integrations](../cloud-guide/integrations/overview.md).

>[!TIP]
>
>For existing Commerce owners migrating to the Cloud infrastructure, learn how to import existing code to the cloud environment.
>
>**Next step**: [Import existing code](import-existing-code.md)
