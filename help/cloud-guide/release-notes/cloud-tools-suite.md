---
title: Release notes for Cloud Tools Suite
description: Learn about the latest improvements to the Cloud Tools suite for Adobe Commerce.
feature: Cloud, Release Notes
exl-id: 6a652e93-46a2-4590-97fc-fb5d114ece9a
---
# Release notes for Commerce Cloud Tools Suite

This release information details the latest improvements to the Cloud Tools Suite for Commerce packages which are designed to deploy and manage Adobe Commerce installations and upgrades on the Cloud platform.

| Release notes     | Version   | Description                              | Source              |
| ----------------- |-----------| ---------------------------------------- | --------------------------- |
| [`ece-tools` package](ece-tools-package.md) | 2002.1.15 | A set of scripts and tools designed to manage and deploy Cloud projects | [`magento/ece-tools`](https://github.com/magento/ece-tools/tree/2002.1) |
| [Cloud Patches for Commerce](cloud-patches.md) | 1.0.23    | A set of patches which improve the integration of all Adobe Commerce versions with Cloud environments. This package includes Adobe Commerce patches and available hotfixes that are applied when you use `ece-tools` to deploy | [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches/tree/1.0.1) |
| [Cloud Docker for Commerce](cloud-docker.md) | 1.3.6     | Functionality and configuration files for Docker images to deploy Adobe Commerce to a local cloud environment | [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker/tree/1.0) |
| [Cloud Components of Commerce](cloud-components.md) | 1.0.13    | Extended Adobe Commerce core functionality for sites deployed on the Cloud infrastructure | [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components/tree/1.0.2) |

When you update to ECE-Tools 2002.1.0 or later, you automatically update to the latest versions of the other packages, which are dependencies for the `ece-tools` package. See [Cloud metapackage](../development/overview.md#cloud-metapackage) for a list of dependencies.
