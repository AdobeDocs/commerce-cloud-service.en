---
title: Technology stack
description: See the technology stack that forms the Commerce on Cloud infrastructure.
feature: Cloud, Iaas, Paas
---
# Technology stack

Think of the Adobe Commerce on cloud infrastructure as five functional layers, as shown below:

![Cloud stack](../../assets/CloudStack.svg)

1. [**Cloud Infrastructure**](pro-architecture.md): Choose either Amazon Web Services (AWS) or Microsoft Azure as your Infrastructure as a Service (IaaS) foundation for your Adobe Commerce on cloud infrastructure Pro projects.
1. [**Platform as a Service**](cloud-architecture.md): Each Adobe Commerce on cloud infrastructure project provides a Platform as a Service (PaaS) Integration environment for developing, testing, and integrating services.
1. [**Adobe Commerce**](../project/overview.md): Adobe Commerce on cloud infrastructure provides a pre-provisioned infrastructure that includes PHP, MySQL (MariaDB), Redis, [!DNL RabbitMQ], and supported search engine technologies.
1. [**Performance Tools**](../monitor/new-relic.md): New Relic performance tools enable you to debug, monitor, and manage your applications and infrastructure by collecting, analyzing, and displaying data from your Adobe Commerce on cloud infrastructure projects.
1. [**Content Delivery Network (CDN), Web Application Firewall ([!DNL WAF]) and Image Optimization (IO)**](../cdn/fastly.md):

   * [Fastly CDN](../cdn/fastly.md#ddos-protection)—Provides secure CDN services with built-in protection from Distributed Denial of Service (DDoS) attacks like [!DNL Ping of Death], [!DNL Smurf] attacks, and other Internet Control Message Protocol (ICMP) based flood attacks.
   * [Web Application Firewall (WAF)](../cdn/fastly-waf-service.md)—WAF services ensure PCI compliance for Adobe Commerce storefronts in Production environments and WAF policies that protect your Adobe Commerce web applications from injection attacks, malicious input, cross-site scripting, data exfiltration, HTTP protocol violations, and other [[!DNL OWASP] Top Ten security threats](https://www.owasp.org/index.php/Top_Ten).
   * [Image optimization (IO)](../cdn/fastly-image-optimization.md)—Provides real-time image manipulation and optimization to speed up image delivery and simplify maintenance of image source sets for responsive web applications. Fastly IO offloads image processing and resizing load, freeing servers to process orders and conversions efficiently.

Monolithic applications are resource-intensive and difficult to scale and serve rapidly. With the Cloud infrastructure, Commerce customers gain unparalleled access to SaaS-based microservices that are rich, intelligent, and performant. See [Supported software and services](cloud-architecture.md#supported-software-and-services).

Use the [Commerce Get Started guide](../../get-started/overview.md) to set up your new Cloud program and begin managing your Commerce application in a cloud-native environment.
