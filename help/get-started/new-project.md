---
title: Initialize Commerce project
description: Learn how to prepare Customer Technical Advisor to provision your Adobe Commerce on cloud infrastructure project.
---
# Initialize Commerce project

Let's get started and initialize your Commerce project on cloud infrastructure!

Before Adobe provisions your cloud project environments, it is recommended that you consider the following strategies and prepare answers for your first consult with your Adobe Account Team.

The following is a checklist to help you prepare for your conversation to provision a cloud project:

>[!BEGINSHADEBOX]

- &#9744; [Cloud service strategy](#cloud-service-strategy)
- &#9744; [Domain definition](#domain-definition)
- &#9744; [Transactional email domain](#transactional-email-domain)
- &#9744; [Connection service](#connection-service)
- &#9744; [Storage allocation](#storage-allocation)
- &#9744; [Target site launch](#target-site-launch)

>[!ENDSHADEBOX]

## Cloud service strategy

Adobe Commerce on cloud infrastructure uses Amazon Web Services and Microsoft Azure services. Each service provider operates in multiple regions and provides multiple availability zones. Choosing a region convenient to your location reduces the potential for latency and higher costs.

See [a map of Adobe Commerce cloud regions](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/infrastructure/cloud/regions.html) in the _Implementation Playbook_.

## Domain definition

Prepare to integrate the Fastly and nginx services by defining your top-level domains and subdomains for Pro Staging and any Production environment. You can add domains after the initial setup only by submitting a support ticket, so it is recommended that you have your domains ready.
 
Example for Production and Staging Domains: 

- `www.your-store.com`
- `your-store.com`
- `mcprod.your-store.com`
- `mcstaging.your-store.com`

See [Set up multiple websites or stores](../cloud-guide/store/multiple-sites.md) in the _Commerce on Cloud Infrastructure_ guide for guidance on multiple or unique domains.

## Transactional email domain

Adobe Commerce on Cloud offers SendGrid Simple Mail Transfer Protocol (SMTP) proxy service that provides outbound email authentication and reputation monitoring services. SendGrid sends transactional email on your behalf, so it requires domain information.

Example for SendGrid Domains: `example@your-store.com`

See [SendGrid mail service](../cloud-guide/project/sendgrid.md) in the _Commerce on Cloud Infrastructure_ guide for further guidance about transactional emails and domain settings.

## Connection service

Adobe Commerce on cloud infrastructure supports integration with the AWS PrivateLink or Azure Private Link service. Though this service is optional, PrivateLink is used to establish secure, private communication between cloud infrastructure environments with services and applications hosted on external systems.

It is important to consider your cloud service strategy (AWS or Azure) so that the Adobe Commerce instance is accessible within the same region. See [PrivateLink service](../cloud-guide/development/privatelink-service.md) in the _Commerce on Cloud Infrastructure_ guide for further clarification.

## Storage allocation

Adobe Commerce on cloud infrastructure uses storage for the file structure, search indexing, and the database. You can subdivide the storage as needed beginning with 10 GB for each partition.

The amount of storage you contracted for your cloud project represents the total storage for each environment. For example, if you bought 50 GB of storage space, then you have 50 GB of storage for each environment. There is 50 GB of separate storage for production, staging, and each integration environment respectively.

You can increase your contracted storage at any time. For Pro Production and Staging environments, you must submit an Adobe Commerce Support ticket to change disk space allocation. A size increase of Pro Production and Staging environments can only occur at certain intervals, so, depending on your current disk space usage, support might recommend increasing disk space allocation by a minimum of 10 GB. Once allocated, the storage increase for Pro staging and production can **not** be reverted.

See [Manage disk space](../cloud-guide/storage/manage-disk-space.md) in the _Commerce on Cloud Infrastructure_ guide.

## Target site launch

Launching a site requires iterative configuration and testing to ensure your site launch success. Setting a target date helps you and your Adobe Account Team to prepare for the final, pre-launch activities, which include a call to coordinate the final steps.

See the [Launch site overview](../cloud-guide/launch/overview.md) in the _Commerce on Cloud Infrastructure_ guide to review the full process and download the Launch checklist.

>[!TIP]
>
> Take a quick look at the Cloud portal and access your new cloud project.
>
>**Next step**: [Onboarding to Commerce](onboarding.md)
