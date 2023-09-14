---
title: Prepare your workspace
description: Gather credentials and learn about the tools available to set up a development workspace for use with your Commerce on cloud infrastructure project.
recommendations: noDisplay, catalog
---

# Prepare your workspace

Whether you are new to Commerce or are an existing Commerce owner moving to the cloud infrastructure, use these steps to guide you in preparing a development workspace for your Cloud project. If you already completed some of these steps or have an existing Adobe Commerce developer environment, review the following for expected results and continue to the next step. Some configurations and workflows differ from a typical on-premises installation.

## Credentials

Before setting up a workspace, gather the following keys and account access:

- **Authentication keys (Composer keys)**

  Authentication keys are 32-character authentication tokens that provide secure access to the Adobe Commerce Composer repository (`repo.magento.com`), and any other Git services required for application development such as GitHub. Your account can have multiple authentication keys. For the workspace setup, start with one specific key for your code repository. If you do not have any keys, contact the project owner, or create the [authentication keys](../cloud-guide/development/authentication-keys.md) yourself.

- **Cloud Project account**

  The Project Owner should invite you to the Adobe Commerce on cloud infrastructure project. When you receive the e-mail invitation, click the link and follow the prompts to create your account.

- **Adobe Commerce Encryption Key**

  When importing an existing system only, capture the encryption key used to protect your access and data for the database. For details on this key, see [Resolve issues with encryption key](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolve-issues-with-encryption-key.html)

## Developer tools

- **Install the Cloud CLI**

  Install the `magento-cloud` CLI so that you can manage Cloud environments and run automation tasks. See [Cloud CLI](../cloud-guide/dev-tools/cloud-cli-overview.md) for installation instructions.

- **Install Docker for local development and testing**

  Use the Docker environment to emulate the Commerce on cloud infrastructure `integration` environment for local development. You need three essential components: an Adobe Commerce v2 template, Docker Compose, and `ece-tools` package.

  - [Docker architecture and common commands](../cloud-guide/dev-tools/cloud-docker.md)
  - [Launch Docker development environment](https://developer.adobe.com/commerce/cloud-tools/docker/setup/)
  - [ECE-Tools package](../cloud-guide/dev-tools/package-overview.md)

- **Integrate Git-based services**

  Optionally integrate a Git-based hosting service, such as GitHub or GitLab, with Adobe Commerce on cloud infrastructure. See [Integrations](../cloud-guide/integrations/overview.md).
