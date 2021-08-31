---
title: Architecture for Commerce on AEC
description: Describes the architecture for Commerce on the Adobe cloud infrastructure.
---

# Architecture for Commerce on AEC

The Commerce platform architecture, built on Ethos-Kubernetes and Adobe Cloud technology, provides a cloud-native hosting environment with self-service capabilities.

>[!IMPORTANT]
>
>Insert tech stack diagram

## Infrastructure

- **Ethos-Kubernetes**—Ethos-managed clusters and Kubernetes operators orchestrate the Commerce stack and provide a stateless, read-only environment including:

  - **Contour**—ingress controller, load balancer with routing and SSL termination
  - **NGINX**—web server with PHP binaries
  - **PHP**—command-line capabilities
  - Secrets management

- **Skyline Cloud Controller**—

- [!DNL **AWS Managed Services**]—Provides a high-availability operational structure that includes the following services required to support Commerce.

  - **Aurora**—A fault-tolerant, relational database compatible with MySQL.
  - **Elasticsearch**—Powerful, multi-tenant search engine.
  - **RabbitMQ**—A native message queue for Commerce that enables a module to publish messages to queues and consumers to receive messages asynchronously.
  - **Redis**—(ElastiCache) session and search caching.
  - **S3**—Simple storage service that provides the option to store files and schedule imports/exports in a persistent, remote storage container that is version controlled, backed up, and encrypted.

- **Git**—Each Commerce program uses a Git-based source repository.

## Software

- **Cloud Manager**—Cloud Manager provides a basis for the new Commerce Program UI and includes self-service mechanisms for the following:

  - Environment access, variables, and controls
  - CICD Pipeline optimization and scheduling
  - Activity and performance monitoring
  - Git source repository access management
  - Domain settings and allowlist management

  See the [Cloud Manager documentation][].

- **Admin Console**—Control team access to the Commerce program and define roles.

- **Third-party integration**—

  - [Fastly][]—CDN service, WAF management, image optimization, and other security features.
  - [New Relic][]—Software analytics service for analyzing Commerce interactions, such as database queries, customer transactions, and application dependency and event monitoring.
  - [SendGrid][]—SMTP proxy service provides email authentication and reputation monitoring.


<!-- link definitions -->
[Cloud Manager documentation]: https://www.adobe.io/apis/experiencecloud/cloud-manager.html
[Fastly]: https://www.fastly.com
[New Relic]: https://newrelic.com
[SendGrid]: https://sendgrid.com
