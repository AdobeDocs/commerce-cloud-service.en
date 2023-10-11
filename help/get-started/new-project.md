---
title: Provision Commerce on Cloud
description: Learn how to prepare an Adobe Customer Technical Advisor to provision your Adobe Commerce on cloud infrastructure project.
recommendations: noDisplay, catalog
role: Admin
exl-id: cfb354b0-c255-4b6e-94aa-c5a6bf7230d6
---
# Commerce on Cloud provisioning prerequisites

Let's get started and initialize your Commerce project on cloud infrastructure!

Before Adobe provisions your Commerce on cloud project environments, it is recommended that you consider the following strategies and prepare answers for your first consult with your Adobe Account Team. Use the following sections as a checklist to help you prepare for your conversation with a Customer Technical Advisor to provision a cloud project:

## Domain definition

**Question 1**: _What domain or domains do you intend to use for site launch?_

Prepare to integrate the Fastly and nginx services by defining your top-level domains and subdomains for the Pro Staging and Production environments. After the initial setup, you can only add domains by submitting an Adobe Commerce Support ticket, so it is recommended that you have your domain information ready.
 
Examples for Production and Staging domains: 

- `www.your-store.com`
- `your-store.com`
- `mcprod.your-store.com`
- `mcstaging.your-store.com`

See [Set up multiple websites or stores](../cloud-guide/store/multiple-sites.md) in the _Commerce on Cloud Infrastructure_ guide for further guidance on multiple or unique domains.

## Transactional email domain

**Question 2**: _Which domain or domains do you intend to use for transactional emails?_

Adobe Commerce on Cloud uses the SendGrid Simple Mail Transfer Protocol (SMTP) proxy service, which provides outbound email authentication and reputation monitoring services. SendGrid sends transactional emails on your behalf, so it requires domain information.

Example for SendGrid domain: `example@your-store.com`

See [SendGrid mail service](../cloud-guide/project/sendgrid.md) in the _Commerce on Cloud Infrastructure_ guide for further guidance about transactional emails and domain settings.

## Storage allocation

**Question 3**: _How much of your contracted storage do you plan to allocate for file upload and for database?_

Adobe Commerce on cloud infrastructure uses storage for the file structure, search indexing, and the database. You can subdivide the storage as needed beginning with 10 GB for each partition.

The amount of storage you contracted for your cloud project represents the total storage for each environment. For example, if you bought 50 GB of storage space, then you have 50 GB of storage for each environment. There is 50 GB of separate storage for production, staging, and each integration environment respectively.

You can increase your contracted storage at any time. For Pro Production and Staging environments, you must submit an Adobe Commerce Support ticket to change disk space allocation. A size increase of Pro Production and Staging environments can only occur at certain intervals. Depending on your current disk space usage, the support team might recommend increasing disk space allocation by a minimum of 10 GB. Once allocated, the storage increase for Pro Staging and Production can **not** be reverted.

See [Manage disk space](../cloud-guide/storage/manage-disk-space.md) in the _Commerce on Cloud Infrastructure_ guide.

## Cloud service region

**Question 4**: _Which Cloud service region is most convenient to your proximity?_

Choose either Amazon Web Services (AWS) or Microsoft Azure as your Infrastructure as a Service (IaaS) foundation for your Adobe Commerce on cloud infrastructure Pro projects. Each service provider operates in multiple regions and provides multiple availability zones. Select a region convenient to your location and reduce the potential for latency and higher costs.

See [a map of Adobe Commerce cloud regions](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/infrastructure/cloud/regions.html) in the _Implementation Playbook_.

## Connection service

**Question 5**: _Do you need a PrivateLink service? If so, in which region is the PrivateLink connection?_

Adobe Commerce on cloud infrastructure supports integration with the AWS PrivateLink or Azure Private Link service. Though this service is optional, PrivateLink is used to establish secure, private communication between cloud infrastructure environments with services and applications hosted on external systems.

It is important to consider your cloud service strategy (AWS or Azure) so that the Adobe Commerce instance is accessible within the same region. See [PrivateLink service](../cloud-guide/development/privatelink-service.md) in the _Commerce on Cloud Infrastructure_ guide for further clarification about regional accessibility.

## Target site launch

**Question 6**: _What is your projected target launch date?_

Launching a site requires iterative configuration and testing to ensure your site launch success. Setting a target date helps you and your Adobe Account Team to prepare for the final, pre-launch activities, which include a call to coordinate the final steps.

See the [Launch site overview](../cloud-guide/launch/overview.md) in the _Commerce on Cloud Infrastructure_ guide to review the full process and download a copy of the Launch checklist.

>[!TIP]
>
> Take a quick look at the Cloud portal and access your new cloud project.
>
>**Next step**: [Onboarding to Commerce](onboarding.md)
