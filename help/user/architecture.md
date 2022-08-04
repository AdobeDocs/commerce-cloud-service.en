---
title: Architecture for Commerce on cloud infrastructure
description: Describes the architecture for Commerce on the cloud infrastructure.
---

# Commerce architecture

The Commerce platform architecture, built on Ethos-Kubernetes and Adobe Experience Cloud technology, provides a cloud-native hosting environment with self-service capabilities.

## Tools and integrations

- [Fastly][]—CDN service, WAF management, image optimization, and other security features.
- [New Relic][]—Software analytics service for analyzing Commerce interactions, such as database queries, customer transactions, and application dependency and event monitoring.
- [SendGrid][]—SMTP proxy service provides email authentication and reputation monitoring.

## Infrastructure

- **[!DNL AWS Managed Services]**—Provides a high-availability operational structure that includes the following services required to support Commerce:

  - **Aurora**—A fault-tolerant, relational database compatible with MySQL.
  - **Elasticsearch**—Powerful, multi-tenant search engine.
  - **RabbitMQ**—A native message queue for Commerce that enables a module to publish messages to queues and consumers to receive messages asynchronously.
  - **Redis**—(ElastiCache) session and search caching.
  - **S3**—Simple storage service that provides the option to store files and schedule imports/exports in a persistent, remote storage container that is version controlled, backed up, and encrypted.

- **Git**—Each Commerce program uses a Git-based source repository.

<!-- link definitions -->

[Fastly]: https://www.fastly.com
[New Relic]: https://newrelic.com
[SendGrid]: https://sendgrid.com
