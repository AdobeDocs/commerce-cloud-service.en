---
title: Commerce Platform Architecture
description: Describes the infrastructure for the Commerce Platform solution.
exl-id: 0dd3bd1b-e530-4436-b6c6-90f9f508e8a6
---

# Commerce on AEC Architecture

The Commerce platform architecture is built on Ethos-Kubernetes and Adobe Cloud Manager to provide a cloud-native hosting environment with self-service capabilities.

- **Ethos-Kubernetes**—Platform-as-a-service Ethos-managed clusters and kubernetes operators orchestrate the Commerce stack.

- **Cloud Manager**—Cloud Manager provides a basis for the new Commerce Program UI.

  - Environment access and controls
  - CICD Pipeline optimization and scheduling
  - Git management and activity logs
  - Performance monitoring

  See the [Cloud Manager documentation][].

- **Admin Console**—Control access to the Commerce program and define roles.
- **Commerce**—The Commerce application is powered by Magento.

<!-- link definitions -->
[Cloud Manager documentation]: https://www.adobe.io/apis/experiencecloud/cloud-manager.html
