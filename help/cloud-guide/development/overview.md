---
title: Development overview
description: Prepare for local development with an Adobe Commerce on cloud infrastructure project.
---

# Development overview

Adobe Commerce on cloud infrastructure remote environments are **Read Only**, including all Starter environments and all Pro Integration, Staging, and Production environments. In a local development environment, you can write and test code before pushing it to an Integration environment for further testing and deployment to Staging and Production.

## Development packages

Adobe Commerce on cloud infrastructure uses Composer to manage the dependencies and upgrades for projects. Composer installs the required libraries and dependencies for your project in the `vendor` directory. The following required Composer files are in the project root directory:

- `composer.json`—Use the `composer.json` file to manage product installations and upgrades.
- `composer.lock`—The `composer.lock` file stores a set of exact version dependencies that satisfy the version constraints of every requirement for every package in the dependency tree of the project.

**Common commands:**

| Command            | Description                                                                                                                                              |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update`  | Updates to the latest versions of the dependencies reflected in the `composer.json` file. This updates the `composer.lock` file.                         |
| `composer install` | Reads the `composer.lock` file to download dependencies. It is a best practice to keep an up-to-date copy of `composer.lock` in your project repository. |

Once you add, commit, and push the updated code, the deployment process automatically runs the `composer install` command during the [build phase](../deploy/process.md#build-phase-build-phase).

### Cloud metapackage

Adobe Commerce on cloud infrastructure uses a metapackage that requires `magento/product-enterprise-edition`. To get the latest updates for latest version of Commerce, use the following constraint syntax:

```text
>=current_version <next_version
```

For example, to use the latest Adobe Commerce version 2.4.5, set `2.4.5` as the "current" version and `2.4.6` as the "next" version in the `composer.json` file:

```text
"magento/magento-cloud-metapackage": ">=2.4.5 <2.4.6"
```

The main packages of this metapackage are the following:

-  **vendor/magento/ece-tools**—The `ece-tools` package is compatible with Adobe Commerce version 2.1.4 and later to provide a rich set of features you can use to manage your Adobe Commerce on cloud infrastructure project. It contains scripts and Adobe Commerce on cloud infrastructure commands designed to help manage your code and automatically build and deploy your projects. See [Ece-tools package overview](../dev-tools/package-overview.md).
-  **vendor/magento/product-enterprise-edition**—This metapackage requires application components, including modules, frameworks, themes, and so on.
-  **vendor/fastly2/magento2**—This module manages the Fastly CDN and services for the Pro Staging and Production and Starter Production environments. See [Fastly services](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
-  **vendor/magento/module-paypal-on-boarding**—This module provides PayPal payment gateway checkout by connecting to your PayPal merchant account. See [PayPal On-Boarding tool](../store/paypal.md).

## Gather credentials

Before setting up a workspace, gather the following credentials and accounts:

-  **Authentication keys (Composer keys)**

    Authentication keys are 32-character authentication tokens that provide secure access to the Adobe Commerce Composer repository (repo.magento.com), and any other Git services required for application development such as GitHub. Your account can have multiple authentication keys. For the workspace setup, start with one specific key for your code repository. If you do not have any keys, contact the Account Owner to create them, or create the [authentication keys](authentication-keys.md) yourself.

-  **Cloud Project account**

    The Account Owner or Technical Admin (Super User) should invite you to the Adobe Commerce on cloud infrastructure project. When you receive the e-mail invitation, click the link and follow the prompts to create your account. See [Onboarding](../../get-started/onboarding.md) or [Access the Project Web Interface](../project/overview.md) for details.

-  **Adobe Commerce Encryption Key**

    When importing an existing system only, capture the encryption key used to protect your access and data for the database. For details on this key, see [Resolve issues with encryption key](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolve-issues-with-encryption-key.html)

## Launch a Docker environment

You can use the Docker environment to emulate the Adobe Commerce on cloud infrastructure Integration environment for local development. You need three essential components: an Adobe Commerce v2 template, Docker Compose, and Adobe Commerce on cloud infrastructure `ece-tools` package.

-  [Docker architecture and common commands](https://devdocs.magento.com/cloud/docker/docker-development.html)
-  [Launch Docker development environment](https://devdocs.magento.com/cloud/docker/docker-config.html)

>[!TIP]
>
>For information about using Git-based hosting services with Adobe Commerce on cloud infrastructure, see [Integrations](../integrations/overview.md).
