---
title: Release notes for Cloud Suite
description: Learn about the latest improvements to the Cloud suite.
---

# Release notes for Cloud Suite

This release information details the latest improvements to the Cloud Suite for Commerce packages which are designed to deploy and manage Adobe Commerce installations and upgrades on the Cloud platform.

| Release notes     | Version              | Description                              | Source              |
| ----------------- | -------------------- | ---------------------------------------- | --------------------------- |
| [`ece-tools`](ece-release-notes.md) | 2002.1.12<br/>2002.0.23 | A set of scripts and tools designed to manage and deploy Cloud projects | [`magento/ece-tools`](https://github.com/magento/ece-tools/tree/2002.1) |
| [Cloud Patches for Commerce](mcp-release-notes.md) | 1.0.19 | A set of patches which improve the integration of all Adobe Commerce versions with Cloud environments. This package includes Adobe Commerce patches and available hotfixes that are applied when you use `ece-tools` to deploy | [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches/tree/1.0.1) |
| [Cloud Docker for Commerce](mcd-release-notes.md) | 1.3.3 | Functionality and configuration files for Docker images to deploy Adobe Commerce to a local cloud environment | [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker/tree/1.0) |
| [Cloud Components of Commerce](mcc-release-notes.md) | 1.0.12 | Extended Adobe Commerce core functionality for sites deployed on the Cloud infrastructure | [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components/tree/1.0.2) |

When you update to `ece-tools` 2002.1.0 or later, you automatically update to the latest versions of the other packages, which are dependencies for `ece-tools`.
